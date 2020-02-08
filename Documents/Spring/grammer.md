

## 1. 전역변수

gradle에서는 전역변수를 사용하기 위해서 `ext{ ... }` 를 이용합니다.

```groovy
// build.gradle 내부 예시
buildscript{
  ext{
    springBootVersion = '2.1.7.RELEASE'
  }
  dependencies{
        classpath("org.springframework.boot:spring-boot-gradle-plugin:${springBootVersion}")
   }
}
```

이는 `springBootVersion`을 '2.1.7.RELEASE'이라는 값을 가지는 전역변수로 생성하고, spring-boot-gradle-plugin이라는 스프링 부트 그레이들 플러그인의 2.1.7.RELEASE를 의존성으로 받겠다는 의미입니다.



## 2. 플러그인 추가



```groovy
apply plugin : 'java'
apply plugin : 'eclipse'
apply plugin : 'org.springframework.boot'
apply plugin : 'io.spring.dependency-management'
```

각각 뒤에 있는 ``'java'``, `` 'eclipse'``, `` 'org.springframework.boot' ` , `'io.spring.dependency-management'` 를 플러그인으로서 추가한다는 의미입니다. 위 예시는 자바와 스프링부트를 사용하기 위해서는 필수 플러그인입니다. 