# ecommerce-msa-config
[ecommerce-msa 프로젝트](https://github.com/gr1993/ecommerce-msa)의 Spring Boot 서비스 설정을 관리하는 Git 저장소로, Config Server가 이 저장소를 참조하도록 구성된다.


### 설정 파일 구조

```
config-repo/
├── application.yml                # 모든 서비스 공통
├── application-dev.yml            # dev 공통
├── application-prod.yml           # prod 공통
│
├── user-service.yml
├── user-service-dev.yml
├── user-service-prod.yml
...
```

만약 user-service가 dev 프로필로 Config Server에 설정 파일을 요청하면, Config Server는  
여러 설정 파일을 순서대로 병합하여 최종 설정을 제공한다.  
최종적으로 동일한 키가 여러 파일에 존재하면, **나중에 읽은 파일의 값이 우선 적용**된다.

#### 설정 파일 병합 순서
1. application.yml – 모든 서비스에 공통으로 적용되는 기본 설정
2. application-dev.yml – 모든 서비스에 적용되는 dev 프로필 전용 설정
3. user-service.yml – user-service 전용 공통 설정
4. user-service-dev.yml – user-service 전용 dev 프로필 설정