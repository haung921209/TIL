# 샤딩

## 샤딩이란

샤딩은 "조각내다"라는 뜻으로 데이터베이스 저장기법 중 하나이며, 전체 네트워크를 분할한 뒤 트랜잭션을 영역별로 저장하고 이를 병렬적으로 처리하는 방법.

수직적으로 나누는 정규화 등의 기법과는 다르게, 수평적으로 나누는 방법.

## 내가 적용한 환경

- Java 1.8
- Spring Boot Starter 2.1.12
- MyBatis 2.1.1
- MySQL

## 적용한 이유

NHN Toast Rookies 7기 Basecamp 메일 서비스(쓸 수록 행복해져요, HappyMail! 이하 해피메일)을 만들던 중, 샤드 과제를 받았기 때문.

## 적용한 방법

### 0. 사전 지식

현 해피메일 서비스는 데이터베이스에 유저 정보와, 이와 연관된 메일 정보, 파일 정보 등을 저장하고 있다. 그리고 그 유저 정보에는 아이디, 이름, 비밀번호(암호화), 두레이 URL(메일 수신 / 발신 시에 Hook을 이용하기 위함. 선택정보)을 저장하고 있다. 이 중, 아이디의 경우에는 unique하기 때문에 이를 이용하여 샤드를 나누는 방법을 택했다.
유저 아이디는 String으로 저장이 되어있다. 그리고 Java는 String에 대해서 hashCode를 계산하는 메소드를 가지고 있다. 

```JAVA
s.hashCode() == s[0]*31^(n-1) + s[1]*31^(n-2) + ... + s[n-1] //해시코드 계산식
```
이 값은 유일성을 보장하지는 않지만, 짝/홀에 대해서는 같은 String에 대하여 같은 값을 보장하기 때문에 샤드를 나눌 때 아이디 값의 hashCode값을 계산해서, 짝 / 홀에 대해 각각 샤드가 나눠질 수 있도록 구분하였다.

### 1. DataSourceConfig.java

```JAVA
package com.nhn.happy.mail.config;

import java.util.HashMap;
import java.util.Map;

import javax.sql.DataSource;

import org.slf4j.Logger;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.beans.factory.annotation.Qualifier;
import org.springframework.boot.autoconfigure.jdbc.DataSourceProperties;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.Primary;
import org.springframework.jdbc.datasource.lookup.AbstractRoutingDataSource;

import com.fasterxml.jackson.databind.ObjectMapper;
import com.nhn.happy.mail.MultiRoutingDataSource;
import com.nhn.happy.mail.util.DatabaseSelector;
import com.nhn.happy.mail.util.RestTemplateUtil;
import com.nhn.happy.mail.util.SelectDatabaseUtil;
import com.nhn.happy.mail.vo.SecretKeyResponse;
import com.zaxxer.hikari.HikariDataSource;


@Configuration
public class DataSourceConfig {

	@Autowired
	DatabaseSelector databaseSelector;

	@Autowired
	SelectDatabaseUtil selectDatabaseUtil;
	@Autowired
	RestTemplateUtil rt;
	@Autowired
	ObjectMapper objectMapper;
	@Autowired
	Logger log;

	@Bean(name = "db01Datasource")
	public HikariDataSource firstDataSource() {
		SecretKeyResponse databaseKey = rt.getFirstDatabaseKey();
		DataSourceProperties dataSourceProperties = selectDatabaseUtil.datasourceGenerator(databaseKey);
		if(dataSourceProperties==null)
			return null;
		return dataSourceProperties.initializeDataSourceBuilder().type(HikariDataSource.class).build();
	}

	@Bean(name = "db02Datasource")
	public HikariDataSource secondDataSource() {
		SecretKeyResponse databaseKey = rt.getSecondDatabaseKey();
		DataSourceProperties dataSourceProperties = selectDatabaseUtil.datasourceGenerator(databaseKey);
		if(dataSourceProperties==null)
			return null;
		return dataSourceProperties.initializeDataSourceBuilder().type(HikariDataSource.class).build();
		
	}

	@Bean
	@Primary
	public DataSource createRoutingDatasource(@Autowired @Qualifier("db01Datasource") DataSource firstDataSource,
			@Autowired @Qualifier("db02Datasource") DataSource secondDataSource) {
		AbstractRoutingDataSource routingDataSource = new MultiRoutingDataSource();

		Map<Object, Object> targetDataSources = new HashMap<>();
		targetDataSources.put("db01", firstDataSource);
		targetDataSources.put("db02", secondDataSource);

		databaseSelector.addDatabaseKey("db01");
		databaseSelector.addDatabaseKey("db02");

		routingDataSource.setTargetDataSources(targetDataSources);

		return routingDataSource;
	}
}


```

- firstDataSource / secondDataSource 메소드
  - 먼저, 현재 프로젝트에서는 datasource에 대해서 username, password, url값만 설정해서 사용하고 있다. 그리고 우리 프로젝트에서는 Toast Cloud Secure Key Manager를 이용하여 해당 값을 관리하고 있다.
    ```JAVA
		SecretKeyResponse databaseKey = rt.getSecondDatabaseKey();
    ``` 
    위 부분은 RestTemplate을 이용, 해당 키 값을 받아오는 부분이다. 
  - 그리고
    ```JAVA
    DataSourceProperties dataSourceProperties = selectDatabaseUtil.datasourceGenerator(databaseKey);
    return dataSourceProperties.initializeDataSourceBuilder().type(HikariDataSource.class).build();
    ```
    해당 부분은 위에서 받아온 키 값을 이용, DataSourceProperties를 생성 후, 이를 HikariDataSource로 return하는 코드이다.

  - initializeDataSourceBuilder()의 경우, username, pwd, url값과 함께 타입을 설정해주려고 시도하면 다른 모든 값을 다 필요로 하기 때문에, 먼저 SelectDatabaseUtil에서 설정해주고 그 값에 타입을 넣어주는 방식으로 설정해주었다.

### 2. createRoutingDatasource 메소드
  - 먼저, AbstractDataSource에서 현재 바라보는 datasource가 어딘지 체크한다.

    ```JAVA
    AbstractRoutingDataSource routingDataSource = new MultiRoutingDataSource();
    ```

    ```JAVA
    package com.nhn.happy.mail;

    import org.springframework.beans.factory.annotation.Autowired;
    import org.springframework.jdbc.datasource.lookup.AbstractRoutingDataSource;

    import com.nhn.happy.mail.util.DatabaseSelector;

    import lombok.extern.slf4j.Slf4j;

    @Slf4j
    public class MultiRoutingDataSource extends AbstractRoutingDataSource {

        @Autowired
        private DatabaseSelector databaseSelector;

        @Override
        protected Object determineCurrentLookupKey() {
            Object dbKey = databaseSelector.getDataSource();
            log.debug("[RoutingDataSource] dbKey:{}", dbKey);
            if (dbKey == null)
                return "db01";
            return dbKey;
        }
    }
    ```

    - AbstractRoutingDataSource에는, determineCurrentLookupKey()라는 메소드가 추상 메소드로서 존재한다. 따라서, 이를 상속받아 어떤 datasource를 볼지를 결정해줄 수 있도록 메소드를 작성해주어야 한다. 

    - DatabaseSelector는 `ThreadLocal<String>`으로 database 키를 저장하여 database가 어떤 것이 선택되야 할지를 결정해준다. 해당 코드는 다음과 같다

    ```JAVA

    package com.nhn.happy.mail.util;

    import java.util.ArrayList;
    import java.util.List;

    import org.springframework.stereotype.Component;

    @Component
    public class DatabaseSelector {
        public static final String DB_KEY = "db_key";
        public static final String DB01 = "db01";
        public static final String DB02 = "db02";

        private ThreadLocal<String> contextHolder = new ThreadLocal<>();
        private List<String> databaseKeys = new ArrayList<>();

        public String getDataSource() {
            return contextHolder.get();
        }

        public void setDataSource(String key) {
            contextHolder.set(key);
        }

        public void setDbIndicator(String userId) {
            setDataSource(getDbIndicator(userId));
        }

        public void removeDataSource() {
            contextHolder.remove();
        }

        public void addDatabaseKey(String key) {
            databaseKeys.add(key);
        }

        public List<String> getDatabaseKeys() {
            return databaseKeys;
        }

        public final String getDbIndicator(String userId) {
            if (userId == null) { 
                return DB01;
            }
            if (userId.hashCode() % 2 == 0) {
                return DB01;
            }
            return DB02;
        }
    }
    ```


### 3. 그 외 설정
  - Spring에서는, 하나의 데이터베이스를 기본적으로 선택하게 되어있다. 따러서, 위와 같은 설정을 해준 경우 database 한개를 필요로 하는데 여러개가 주입되게 되므로, 어떤 데이터베이스를 선택해야 하는지 몰라 에러를 내보내게 된다. 따라서, Datasource를 선택하는 것을 자동 설정에서 제외해주는 설정이 필요하다.

    ```JAVA

    package com.nhn.happy.mail;

    import org.springframework.boot.SpringApplication;
    import org.springframework.boot.autoconfigure.EnableAutoConfiguration;
    import org.springframework.boot.autoconfigure.SpringBootApplication;
    import org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration;
    import org.springframework.boot.autoconfigure.jdbc.DataSourceTransactionManagerAutoConfiguration;
    import org.springframework.scheduling.annotation.EnableScheduling;

    @EnableScheduling
    @SpringBootApplication
    @EnableAutoConfiguration(exclude = { DataSourceTransactionManagerAutoConfiguration.class,
            DataSourceAutoConfiguration.class })
    public class MailApplication {
        public static void main(String[] args) {
            SpringApplication.run(MailApplication.class, args);
        }
    }
    ```

    - 해당 부분은 Spring Application이 시작하는 지점이다.   
        ```JAVA 
        @EnableAutoConfiguration(exclude = { DataSourceTransactionManagerAutoConfiguration.class,
                    DataSourceAutoConfiguration.class }) 
        ```
    - 위의 코드가 Spring이 자동으로 Datasource를 처다보지 못하게 하고, AbstractRoutingDatasource의 determineCurrentLookupKey()가 바라보고 있는 datasource를 확인하여 Datasource를 확인할 수 있도록 한다.

### 4. 활용 방법
- Datasource를 선택하는 Service 단에서의 mapper 호출시에, datasource를 바꿔주는 방식으로 진행하였다.
  
  ```JAVA
    @Override
	public MailEntity selectOneMail(String userAddress,int id) {
		databaseSelector.setDbIndicator(userAddress);
		return mailMapper.selectOneSend(id);
	} 
  ```
- 메일 하나를 선택하는 서비스 메소드이다. 이런 방식으로, databaseSelector에서, userAddress를 이용하여 db를 바꾸고, mapper에서 값을 호출하는 방식을 사용했다.


## Side Effect

### 1. 동기화 문제

- 동기화 문제가 팀원으로부터 제기되었다. 
- `A가 service에서 datasource 바꿈 -> B가 service에서 datasource를 바꿈 -> A가 mapper 호출` 과 같은 방식을 취할 경우, A가 원했던 datasource가 아닌, B의 datasource로 잘못 호출될 수 있다는 이유였다.
- 해당 문제에 대한 정확한 인식 없이, 임계구역을 설정해주기 위해 mapper 호출하는 곳에 `@Synchronized`를 달아주었다.
- 결과적으로, Spring에서는 해당 Side effect는 생각할 필요가 없다.
- 왜냐하면, Spring의 경우, 호출에 대해 Thread 독립적으로 실행되기 때문이다.
- Thread 독립적이지 않은 것은 Bean에 대해서인데, 따라서 Bean의 지역변수를 설정하는데 있어서는 조심할 필요가 있다.
- 또한, AbstractDatasource에서 datasource를 바꿔주는 부분에는 이미 `@Synchronized`를 통해 임계구역이 설정되어있기 때문에, 걱정할 필요 없이 진행하면 된다.