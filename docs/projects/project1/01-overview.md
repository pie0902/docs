---
title: 프로젝트 소개
---

# 프로젝트 소개

## 10-trillion-dollars  
**다양한 상품과 편리한 기능으로 사용자 경험을 극대화한 이커머스 플랫폼**

이 프로젝트는 상품 조회/검색, 주문, 결제, 리뷰, 유저 관리 등  
쇼핑몰 서비스의 필수 기능을 모두 포함한 **풀스택 이커머스 애플리케이션**입니다.  
AWS 기반 MSA 아키텍처, Redis 동시성 제어, S3 이미지 처리, ELK 로그 분석 등  
실제 서비스 환경에 가까운 구조로 설계된 프로젝트입니다.

- **배포 사이트 바로가기**
  - https://msa.thunderdev.site/

---

## 프로젝트 정보  
- **개발 기간** : 
    - 24.03.26 ~ 24.04.30 [1차 개발 및 배포]
    - 25.11.30 ~ 25.12.15 [인프라 리팩토링]

- **GitHub** : 
    - https://github.com/10-trillion-dollars  

- **Personal Refactoring GitHub**
  - https://github.com/pie0902/e-commerce
  - (온프레미스 환경 전환, 배포/인프라 구조 재설계)

- **발표 영상 (본인)** : https://www.youtube.com/watch?v=Dve_EWAOOHM  

---

## 팀 구성 및 역할

| 이름 | 담당 |
|------|------|
| 전석배 | 상품 도메인, MSA 구성, ELK, FRONT |
| 주준호 | 유저 도메인, CI/CD 구축, Docker, HTTPS, 쿼리 개선 |
| **윤종일** | **리뷰 도메인, 캐싱, 동시성 제어, FRONT, AWS SES** |
| 박수민 | 주소 도메인, CI/CD, Docker, HTTPS, 부하 테스트 |
| 손영효 | 주문 도메인, S3, 결제 모듈(카카오 API), 테스트 코드(E2E) |

---

## 내가 기여한 핵심 기능 (윤종일)

- **리뷰 도메인 전체 설계 및 API 개발**
- **Redis 기반 캐싱 도입 및 동시성 제어(재고/주문 안정성 강화)**
- **AWS SES 기반 주문 실패 고객 이메일 알림 기능 구현**
- **프론트엔드 리뷰/상품 UI 개발**

---

## 주요 기술 요약

- **Redis 분산락 기반 주문 동시성 제어**
- **상품 목록 Redis 캐싱으로 조회 성능 향상**
- **카카오 결제 모듈(kakao-pay) 연동**
- **GitHub Actions + Docker 기반 CI/CD 구축**
- **MSA 아키텍처 구성 + API Gateway 적용**
- **ELK Stack 기반 로그 수집/분석 및 실시간 Alerting**

---

## 개발환경

### Backend

![Java](https://img.shields.io/badge/Java-ED8B00?logo=openjdk&logoColor=white) : 주 언어로 사용되었습니다.  
![Spring](https://img.shields.io/badge/Spring-6DB33F?logo=spring&logoColor=white) : 백엔드 애플리케이션 개발에 사용되었습니다.  
![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-6DB33F?logo=springboot&logoColor=white) : 프로젝트의 메인 프레임워크로 사용되었습니다.  
![Spring Security](https://img.shields.io/badge/Spring%20Security-6DB33F?logo=springsecurity&logoColor=white) : 인증 및 인가 로직 구현에 사용되었습니다.  
![Hibernate](https://img.shields.io/badge/Hibernate-59666C?logo=hibernate&logoColor=white) : JPA 기반 ORM으로 데이터 매핑에 사용되었습니다.  
![MySQL](https://img.shields.io/badge/MySQL-4479A1?logo=mysql&logoColor=white) : 관계형 데이터베이스로 사용되었습니다.  
![Redis](https://img.shields.io/badge/Redis-DC382D?logo=redis&logoColor=white) : 캐싱 및 분산락 적용에 사용되었습니다.  

---

### DevOps / Infra

![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white) : 애플리케이션 컨테이너화에 사용되었습니다.  
![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?logo=githubactions&logoColor=white) : CI/CD 파이프라인 구축에 사용되었습니다.  


---

### AWS

![EC2](https://img.shields.io/badge/AWS-EC2-FF9900?logo=amazonaws&logoColor=white) : 애플리케이션의 서버 호스팅에 사용되었습니다.  
![ECS](https://img.shields.io/badge/AWS-ECS-FF9900?logo=amazonaws&logoColor=white) : Docker 컨테이너 실행 및 관리를 위해 사용되었습니다.  
![ECR](https://img.shields.io/badge/AWS-ECR-FF9900?logo=amazonaws&logoColor=white) : Docker 이미지를 저장하는 레지스트리로 사용되었습니다.  
![Fargate](https://img.shields.io/badge/AWS-Fargate-FF9900?logo=amazonaws&logoColor=white) : 서버리스 방식으로 컨테이너를 실행하기 위해 사용되었습니다.  
![S3](https://img.shields.io/badge/AWS-S3-FF9900?logo=amazonaws&logoColor=white) : 리뷰 이미지 등 정적 파일 저장에 사용되었습니다.  
![RDS](https://img.shields.io/badge/AWS-RDS-527FFF?logo=amazonrds&logoColor=white) : 관계형 데이터베이스 서비스(MySQL)로 사용되었습니다.  
![ElastiCache](https://img.shields.io/badge/AWS-ElastiCache-C925D1?logo=redis&logoColor=white) : Redis 기반 캐싱 및 분산락 구현에 사용되었습니다.  
![Route53](https://img.shields.io/badge/AWS-Route53-8C4FFF?logo=amazonaws&logoColor=white) : 사용자 도메인 관리 및 DNS 라우팅에 사용되었습니다.  
![ELB](https://img.shields.io/badge/AWS-ELB-FF9900?logo=amazonaws&logoColor=white) : 트래픽 로드밸런싱 및 HTTPS 처리에 사용되었습니다.  
![SES](https://img.shields.io/badge/AWS-SES-FF9900?logo=amazonaws&logoColor=white) : 주문 실패 고객에게 이메일 발송 기능을 구현하는 데 사용되었습니다.  

---

### Logging / Search

![Elasticsearch](https://img.shields.io/badge/Elasticsearch-005571?logo=elasticsearch&logoColor=white) : 검색 및 로그 분석을 위해 사용되었습니다.  
![Logstash](https://img.shields.io/badge/Logstash-005571?logo=logstash&logoColor=white) : 서버 로그를 수집·가공하여 Elasticsearch로 전송하는 데 사용되었습니다.  
![Kibana](https://img.shields.io/badge/Kibana-E6006E?logo=kibana&logoColor=white) : 수집된 로그 데이터를 시각화하고 모니터링하는 데 사용되었습니다.  

---

### Frontend

![HTML5](https://img.shields.io/badge/HTML5-E34F26?logo=html5&logoColor=white) : 프론트엔드 구조 설계 및 마크업에 사용되었습니다.  
![CSS3](https://img.shields.io/badge/CSS3-1572B6?logo=css3&logoColor=white) : 스타일링과 UI 컴포넌트 작성에 사용되었습니다.  
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?logo=javascript&logoColor=black) : 동적 페이지 구현 및 API 연동에 사용되었습니다.  
