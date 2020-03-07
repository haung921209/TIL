# Datasource를 선택할 때, Synchronized로 임계영역을 관리하지 않아도 되는 이유

## 1. 문제제기

저희 행복 TF에서는 이번 Sharding 과제를 진행하면서, 동시성 문제에 대해 고민했습니다. 여러 클라이언트로부터 요청이 들어왔을 때, 여러 클라이언트가 각각 다른 서비스(datasource와의 연결을 결정합니다.)를 요청한다면, datasource 접근에 있어 동시성 문제가 있을 것이라고 생각했기 때문입니다.



## 2. 소스 코드

행복 TF에서 데이터 소스를 결정하는 코드의 일부입니다.

```java
	@Bean
	@Primary
	public DataSource createRoutingDatasource(   
			@Autowired @Qualifier("db01Datasource") DataSource firstDataSource,
			@Autowired @Qualifier("db02Datasource") DataSource secondDataSource
			) {
		AbstractRoutingDataSource routingDataSource = new MultiRoutingDataSource ();
			
		Map<Object, Object> targetDataSources = new HashMap<>();
		targetDataSources.put("db01", firstDataSource);
		targetDataSources.put("db02", secondDataSource);

    databaseSelector.addDatabaseKey("db01");
		databaseSelector.addDatabaseKey("db02");
		routingDataSource.setTargetDataSources(targetDataSources);
		
		return routingDataSource;
	}
```

보시는 것처럼, `AbstractRoutingDataSource`를 이용했습니다. `MultiRoutingDataSource`는 `AbstractRoutingDataSource`를 상속받아 `determineCurrentLookupKey()` 메소드를 정의해 주는 방식이고, 현재 보는 키 값은 `ThreadLocal<String>` 으로 저장된 값을 읽어옵니다.



```java
	@Synchronized
	@Override
	public List<FileEntity> selectSendFiles(String userAddress, int sendMailId) {
		databaseSelector.setDbIndicator(userAddress);
		List<FileEntity> list = mailMapper.selectSendFiles(sendMailId);
		list.forEach(FileUtil::setFormatFileSize);
		return list;
	}
```

Mapper를 호출하는 service 코드입니다. 이 코드의 역할은 메일을 읽을 때 mailMapper에서 파일 목록을 불러오는 역할을 가지고 있으며, 저희 TF는 userAddress(주소에서 도메인 제외한 값)의 hashCode값이 짝수 / 홀수인지에 따라 datasource를 나누고 있기 때문에, databaseSelector의 키 값을 설정해주기 위해 사용합니다. 앞의 문제제기에서 제시했던 것 처럼, 저희는 임계영역을 설정할 필요성이 있다고 생각했고 @Synchronized(lombok)를 사용했습니다.

## 3. @Synchronized가 필요 없는 이유

결론부터 말하자면, Spring은 요청에 대해 thread단위로 처리하기 때문입니다. 

