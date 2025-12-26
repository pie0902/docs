---
title: 프로젝트 소개
---

# 프로젝트 소개

## REGO
**근태관리와 휴가관리**
근태관리와 휴가관리 백엔드(ESS). DTO‑only I/O, 엔티티 Setter 금지, 전역 예외 표준화, JWT 무상태 인증을 핵심 원칙으로 설계했습니다.

---

## 프로젝트 정보  
- **개발 기간** : 
  - 25.10.24 ~ 25.12.25

- **GitHub** : 
  - https://github.com/pie0902/rego-backend

- **Swagger UI**
  - http://107.21.56.220:8080/swagger-ui/index.html

  ## 주요 기술 요약
  - 출퇴근 관리: 체크인/체크아웃, 고정/유연 근무 규칙 반영, 지각/조퇴/부족 근무(SHORT_WORK) 판정
  - 휴가 관리: 신청/승인/거절, 반차(0.5) 지원, 주말 제외 일수 계산, 잔여 연차 검증/차감
  - 연차 잔액: 부여/사용/복원, 입사 1년 미만 월 1일 부여 스케줄러(Feature Flag로 선택 활성화)
  - 사용자/회사: 회원가입(대표/사원), 승인/권한, 프로필 이미지 업로드/정적 제공
  - 대시보드: 내 프로필/근태/연차/휴가 통합 조회
  - API 문서: Swagger UI 제공


  ## 설계 하이라이트
  - DTO-only I/O: 컨트롤러는 DTO만 입·출력(엔티티 외부 노출 금지)
  - 엔티티 Setter 금지: 도메인 메서드 기반 상태 전이로 무결성 확보
  - MVC 분리: Controller(입출력) / Service(비즈니스/트랜잭션) / Repository(영속)
  - 전역 예외 표준화: code/message/errors 통일 응답
  - 보안: JWT + 무상태 세션, 메서드 보안(@PreAuthorize)
  - 성능/관측:
    - 요청 단위 쿼리 카운팅 헤더 제공(X-Query-Count 등)
    - Attendance/Leave 목록 조회는 EntityGraph로 N+1 완화
    - 추가 최적화 대상은 Fetch Join/DTO 조회로 확장 예정

  ## DevOps / Infra
  - 로컬: Docker Compose(MySQL)
  - 정적 이미지 서빙: /profile-images/** → 파일시스템 base-path 매핑
    - base-path(로컬 기본): $HOME/IdeaProjects/ess/uploads/profile-images
    - 기본 이미지: base-path/default/default-profile.png
  - 배포(현재): Docker 이미지 빌드/푸시 → EC2에서 docker compose pull/up -d

  ### AWS(현재/계획)
  - 배포 대상: EC2 (권장 base-path: /var/ess/profile-images)
  - 시크릿(현재): .env/환경변수로 관리(JWT/DB 크리덴셜)

  ## 실행/개발 가이드(로컬)
  - DB: docker compose -f compose.yaml up -d (MySQL 8, DB: ess)
  - 설정: application-sample.properties → application.properties
    - 환경변수: DB_USERNAME, DB_PASSWORD, JWT_SECRET(32바이트+), PROFILE_IMAGE_BASE_PATH
  - 실행: ./gradlew bootRun
  - Swagger: /swagger-ui/index.html

  ## 한계/개선 계획
  - 이미지 저장소 S3 전환 및 CDN 도입
  - 조회 성능 최적화(추가 N+1 제거, DTO 조회/Fetch Join 적용 확대)
  - 요청 DTO Bean Validation 확장
  - JWT 만료/갱신 정책 강화


   ## 개발환경

  ### Backend

  ![Java](https://img.shields.io/badge/Java-21-ED8B00?logo=openjdk&logoColor=white) : 주 언어로 사용되었습니다.

  ![Spring](https://img.shields.io/badge/Spring-6.x-6DB33F?logo=spring&logoColor=white) : 백엔드 애플리케이션 개발에 사용되었습니다.

  ![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.5.x-6DB33F?logo=springboot&logoColor=white) : 프로젝트의 메인 프레임워크로 사용되었습니다.
  
  ![Spring Security](https://img.shields.io/badge/Spring%20Security-6.x-6DB33F?logo=springsecurity&logoColor=white) : JWT 기반 인증 및 인가 로직 구현에 사용되었습니다.

  ![Spring Data JPA](https://img.shields.io/badge/Spring%20Data%20JPA-6DB33F?logo=spring&logoColor=white) : JPA Repository 기반 데이터 접근에 사용되었습니다.

  ![Hibernate](https://img.shields.io/badge/Hibernate-6.x-59666C?logo=hibernate&logoColor=white) : JPA 구현체(ORM)로 데이터 매핑에 사용되었습니다.

  ![MySQL](https://img.shields.io/badge/MySQL-8.x-4479A1?logo=mysql&logoColor=white) : 관계형 데이터베이스로 사용되었습니다.

  ![JWT](https://img.shields.io/badge/JWT-JJWT%200.11.x-000000?logo=jsonwebtokens&logoColor=white) : 토큰 발급/검증에 사용되었습니다.

  ![Swagger](https://img.shields.io/badge/OpenAPI-Springdoc%202.8.5-85EA2D?logo=swagger&logoColor=black) : API 문서화 및 테스트에 사용되었습니다.

  ![Lombok](https://img.shields.io/badge/Lombok-CA1B27?logo=lombok&logoColor=white) : 보일러플레이트 코드 감소에 사용되었습니다.

  ![MapStruct](https://img.shields.io/badge/MapStruct-1.5.x-2F74C0?logoColor=white) : 의존성은 추가되어 있으나, 현재 코드에서는 Mapper를 직접 사용하지 않습니다.

  ---

  ### DevOps / Infra

  ![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white) : 애플리케이션 컨테이너화에 사용되었습니다.

  ![Docker Compose](https://img.shields.io/badge/Docker%20Compose-2496ED?logo=docker&logoColor=white) : 로컬/서버 환경 구성 및 실행에 사용되었습니다.

  ![GitHub Actions](https://img.shields.io/badge/GitHub%20Actions-2088FF?logo=githubactions&logoColor=white) : CI/CD 파이프라인 구축에 사용되었습니다.

  ![DockerHub](https://img.shields.io/badge/DockerHub-2496ED?logo=docker&logoColor=white) : 배포 이미지 레지스트리로 사용되었습니다.

  ---

  ### AWS

  ![EC2](https://img.shields.io/badge/AWS-EC2-FF9900?logo=amazonaws&logoColor=white) : 애플리케이션 서버 호스팅에 사용되었습니다.

  ![RDS](https://img.shields.io/badge/AWS-RDS%20(MySQL)-527FFF?logo=amazonrds&logoColor=white) : 운영 DB로 사용되었습니다.

  ---

  ### Logging / Monitoring

  ![SLF4J](https://img.shields.io/badge/SLF4J-Logger-2A2A2A?logoColor=white) : 애플리케이션 로깅에 사용되었습니다.

  ![Hibernate Stats](https://img.shields.io/badge/Hibernate-Statistics-59666C?logo=hibernate&logoColor=white) : 쿼리/통계 기반 성능 분석 옵션으로 사용했습니다(필요 시 활성화).

  ---

