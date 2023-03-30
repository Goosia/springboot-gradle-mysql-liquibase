# Liquibase Task 연결 및 History 사용을 위한 기본 구조

* 프로젝트 정보
```
Java17
Gradle7.6.1
MySQL 5.7
```

* build.gradle 설정 추가
```gradle
plugins {
    ...
    id 'org.liquibase.gradle' version '2.1.1'
    ...
}

dependencies {
    ...
    liquibaseRuntime 'org.liquibase:liquibase-core:4.16.1'
    liquibaseRuntime 'org.liquibase:liquibase-groovy-dsl:3.0.2'
    liquibaseRuntime 'info.picocli:picocli:4.6.1'
    liquibaseRuntime 'mysql:mysql-connector-java:5.1.34'
    ...
}

liquibase {
    activities {
        main {
            changeLogFile 'src/main/resources/db/changelog/db.changelog-master.yaml'
            url 'jdbc:mysql://localhost:3306/db_liquibase?useUnicode=true&characterEncoding=utf-8&useSSL=false&serverTimezone=Asia/Seoul'
            username 'user_liquibase'
            password '1234'
            logLevel 'debug'
        }
    }
}
* 위 설정은 뺄 수 없는 기본 설정입니다.
```

### mysql 계정 만들기
```
    create database db_liquibase;
    create user user_liquibase@localhost identified by '1234';
    grant all privileges on db_liquibase.* to user_liquibase@localhost;
```
