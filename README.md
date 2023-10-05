# 이커머스 플랫폼, MaybeZone



## 목차
[프로젝트 개요](#1-프로젝트-개요) 

[프로젝트 목표 및 설계](#2-프로젝트-목표-및-설계) 

[기술스택](#3-기술스택)  

[서비스 아키텍처 및 기술적 의사결정](#4-서비스-아키텍처-및-기술적-의사결정)  

[트러블슈팅](#5-트러블-슈팅)  

[프로젝트 결과](#6-프로젝트-결과)  

[팀원 및 역할](#7-팀원-및-역할)

* * *  

# 1. 프로젝트 개요

![MaybeZone](https://github.com/challenge-first/About/assets/134407121/2a4a7e82-c399-4b9c-83cc-107eb5a57969)   

- 팀원 : 김동현, 신윤상, 김광일, 유시환
    
- 기간 : 2022년 07월 30일 ~ 09월 07일, 6주 간 진행

- '__이커머스 플랫폼__'을 주제로 한 프로젝트입니다.    
 
- 백엔드 4명으로 구성된 팀입니다.  
  
- MSA 적용, 대규모 트래픽 처리 및 동시성 제어, 소프트웨어 아키텍처 변화 등을 목표로 프로젝트를 진행했습니다.    
  
- [시연 영상](https://youtu.be/2ey6WT7xDc0?si=5JjYzkGk7hrGTJuZ)  

* * *  

# 2. 프로젝트 목표 및 설계


### 프로젝트 목표  

- MSA 전환
  - DDD(도메인 주도 설계)를 바탕으로 분리된 서비스가 유기적으로 소통하는 서비스
  - 이벤트 스토밍 전략으로 바운딩 컨텍스트를 나누는 설계 전략
  - 다른 도메인에 이벤트로 데이터를 전송하는 이벤트 기반 아키텍처
  - OpenFeign, Kafka를 이용한 동기, 비동기 통신

- 인프라, 플랫폼, 애플리케이션 차원에서 필요한 기술 도입
  - 헥사고날 아키텍처를 채택하여 변경에 유연한 아키텍처 전환
  - Zipkin, Micrometer를 활용한 분산 추적 시스템
  - Prometheus, Grafana를 이용한 모니터링 시스템
  - Resilience4J의 CircuitBreaker 패턴을 통해 장애 내성이 있는 서비스 구축
  - Github Action, Docker를 활용한 CI/CD 환경 구축

- 약 1000만건의 대량의 제품 데이터에서 특정 검색 조건으로 빠르게 해당 제품 데이터에 접근
  - 카테고리로 접근할 수 있는 상품 조회
  - 특정 단어가 포함된 검색어를 이용한 유연한 상품 조회

- 각 도메인에서 발생할 수 있는 동시성 제어
  - 비관적 락
  - Redisson 분산 락

- 대용량 트래픽에도 견딜 수 있는 내구성 있는 서버
  - ScaleUp, ScaleOut
  - 대기열 기능


            
### 프로젝트 설계  

  
- [프로젝트 계획 및 설계](https://github.com/challenge-first/About/wiki/Project-%7C-Plan-&-Design)
   
  
- [API 명세서](https://github.com/challenge-first/About/wiki#3-api) 


* * *  
  
# 3. 기술스택

<img src="https://img.shields.io/badge/MSA-232F3E?style=for-the-badge"/> <img src="https://img.shields.io/badge/OpenJDK-232F3E?style=for-the-badge&logo=OpenJDK&logoColor=white"/> <img src="https://img.shields.io/badge/Spring-6DB33F?style=for-the-badge&logo=Spring&logoColor=white"> <img src="https://img.shields.io/badge/Springboot-6DB33F?style=for-the-badge&logo=Springboot&logoColor=white"> <img src="https://img.shields.io/badge/SpringAOP-6DB33F?style=for-the-badge"> <img src="https://img.shields.io/badge/gradle-02303A?style=for-the-badge&logo=gradle&logoColor=white"> <img src="https://img.shields.io/badge/Apache_Kafka-02303A?style=for-the-badge"> <img src="https://img.shields.io/badge/mysql-4479A1?style=for-the-badge&logo=mysql&logoColor=white"> <img src="https://img.shields.io/badge/amazonec2-FF9900?style=for-the-badge&logo=amazonec2&logoColor=white"/> <img src="https://img.shields.io/badge/amazonrds-527FFF?style=for-the-badge&logo=amazonrds&logoColor=white"/> <img src="https://img.shields.io/badge/Zipkin-E69138?style=for-the-badge"/> <img src="https://img.shields.io/badge/Resilience4j-4479A1?style=for-the-badge"/> <img src="https://img.shields.io/badge/redis-DC382D?style=for-the-badge&logo=redis&logoColor=white"/> <img src="https://img.shields.io/badge/JWT-232F3E?style=for-the-badge"> <img src="https://img.shields.io/badge/Jmeter-999999?style=for-the-badge"> <img src="https://img.shields.io/badge/nGrinder-999999?style=for-the-badge"> <img src="https://img.shields.io/badge/Querydsl-4479A1?style=for-the-badge"/> <img src="https://img.shields.io/badge/Prometheus-E69138?style=for-the-badge"/> <img src="https://img.shields.io/badge/Grafana-E69138?style=for-the-badge"/> <img src="https://img.shields.io/badge/GithubAction-527FFF?style=for-the-badge"/> <img src="https://img.shields.io/badge/Docker-527FFF?style=for-the-badge"/>

* * *  

# 4. 서비스 아키텍처 및 기술적 의사결정  

![image](https://github.com/challenge-first/About/assets/134407121/f32017ad-edd1-44d5-a05a-518aede2c933) 

     
- [서비스 아키텍처 및 기술적 의사결정](https://github.com/challenge-first/About/wiki/Project-%7C-Result-1-%E2%80%90-Architecture#1-%EC%84%9C%EB%B9%84%EC%8A%A4-%EC%95%84%ED%82%A4%ED%85%8D%EC%B2%98)

* * *  

# 5. 트러블 슈팅

- [MSA 설계 및 적용](https://github.com/challenge-first/About/wiki/Project-%7C-Troubleshooting#1-msa-%EC%84%A4%EA%B3%84-%EB%B0%8F-%EC%A0%81%EC%9A%A9)

 
- [선착순 이벤트 구현](https://github.com/challenge-first/About/wiki/Project-%7C-Troubleshooting#2-%EC%84%A0%EC%B0%A9%EC%88%9C-%EC%9D%B4%EB%B2%A4%ED%8A%B8-%EA%B5%AC%ED%98%84)

  
- [데이터 검색 및 조회](https://github.com/challenge-first/About/wiki/Project-%7C-Troubleshooting#3-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EA%B2%80%EC%83%89--%EC%A1%B0%ED%9A%8C) 

  
- [동시성 제어](https://github.com/challenge-first/About/wiki/Project-%7C-Troubleshooting#4-%EB%8F%99%EC%8B%9C%EC%84%B1-%EC%A0%9C%EC%96%B4) 

* * *  

# 6. 프로젝트 결과  

- [선착순 이벤트, 데이터 검색 및 조회 성능개선](https://github.com/challenge-first/About/wiki/Project-%7C-Result-2-%E2%80%90--Improvements)

   
- [아키텍처 전환](https://github.com/challenge-first/About/wiki/Project-%7C-Result-1-%E2%80%90-Architecture)

* * *  

# 7. 팀원 및 역할
  

| 이름 | 담당 역할 | 
| --- | --- |
| 김동현(팀장) |  상품 도메인 개발 
| https://github.com/princeton-d |  상품 검색, 조회, 필터, 페이징 성능 개선
|             |  상품 서버 구현 / CI/CD 배포 환경 구성
|             |  모놀리스 초기 디렉토리 구조 설정
|             |  모놀리스에서 상품 검색 및 조회 기능 구현
|             |  Junit, Mockito를 활용한 테스트 구현
|             |  상품 도메인 조회 검색, 필터 기능 구현
|             |  상품 데이터 수집
|             |  Front-End MVP 구현
|             |  Front-End 상품 검색, 조회 구현 |  
|-|-|
| 신윤상 |  상품 데이터 수집
| https://github.com/Dsys1129 |  모놀리스에서 회원 기능 구현
|             |  모놀리스에서 Junit, Mockito를 활용한 Test 코드 작성
|             |  초기 MSA 구조 설계
|             |  APIGatewayServer 구현
|             |  이벤트 도메인 설계
|             |  Redis 및 Kafka 사용하여 이벤트 대기열 서버 및 스케줄러 서버 구현
|             |  이벤트 쿠폰 발급 서버 구현
|             |  회원 서버 구현 / CI/CD 배포 환경 구성
|             |  Jmeter nGrinder를 사용한 테스트 |  
|-|-|
| 김광일 |  상품 데이터 수집
| https://github.com/kki4504 |   모놀리스에서 경매 조회 기능 구현
|             |  모놀리스에서 주문 결제 기능 구현
|             |  모놀리스에서 Junit, Mockito를 활용한 Test 코드 작성
|             |  Jmeter, nGrinder를 활용한 동시성 테스트 / 테스트 모니터링
|             |  Prometheus, Grafana 모니터링 서버 구현
|             |  결제 서버 구현 / CI/CD 배포 환경 구성
|             |  이벤트 도메인 설계
|             |  이벤트 쿠폰 발급 서버 구현
|             |  Redisson 분산 락 사용하여, 이벤트 대기열 서버 구현
|             |  Docker-compose 활용 Kafka 서버 구축
|             |  로그인, 포인트 조회, 포인트 충전, 결제 Front-End 구현 |  
|-|-|           
| 유시환 |  상품 데이터 수집
| https://github.com/Goonerd17 |  모놀리스에서 로깅, Dto, 경매 입찰 기능 구현
|             |  모놀리스에서 Junit, Mockito를 활용한 Test 코드 작성
|             |  전반적인 MSA 및 도메인 주도 설계 수립
|             |  Jmeter를 활용한 동시성 테스트
|             |  경매 도메인 조회/입찰/낙찰 기능 구현
|             |  스프링 AOP를 활용한 로깅 구현
|             |  Zipkin, Micrometer를 활용한 분산추적 기능 구현 및 배포
|             |  Resilience4j를 활용한 CircuitBreaker 패턴 구현
|             |  소프트웨어 아키텍처 변경
|             |  경매, 상품의 카프카 메세지 Producer, Consumer 구현
|             |  상품 상세 조회 Front-End 구현
|             |  경매 조회/낙찰 Front-End 구현 
|             |  Readme, Wiki 작성 |
