---
title: ERD
---

# ERD (Entity Relationship Diagram)

아래는 프로젝트에서 사용한 실제 엔티티 기반의 ERD입니다.

<img src="/img/project1/erd.png" alt="ERD" style={{ width: "90%", maxWidth: "1000px" }} />

---

# 도메인 상세 설명 (Actual Entities)

본 프로젝트는 **외래키(@ManyToOne 등)를 직접 매핑하지 않고**  
**ID(Long) 컬럼을 통해 관계를 관리하는 구조**입니다.  
MSA 또는 서비스 간 독립성을 고려해 **의존성을 최소화하는 설계 방향**입니다.

---

# 1. User (유저)

### 주요 컬럼
- `email` (unique)
- `username`
- `password`
- `role` (USER / ADMIN)

### 관계 (ID 기반)
- 1:N → Address (userId)
- 1:N → Order (userId)
- 1:N → Review (userId)

### 특징
- JPA 연관관계 없이 **userId(Long)** 로만 다른 엔티티와 연결  
- 인증/인가 및 관리자 권한 기능 지원

---

# 2. Address (주소)

### 주요 컬럼
- `city` (시)
- `village` (구)
- `province` (동)
- `userId` (주소 소유 사용자)

### 관계
- N:1 → User (userId)
- 1:N → Order (addressId)

### 특징
- 한 유저가 여러 주소를 가질 수 있음  
- 기본 배송지 기능은 서비스 레이어에서 관리

---

# 3. Product (상품)

### 주요 컬럼
- `name` : 상품명  
- `price`  
- `description`  
- `stock` : 재고  
- `imageUrl` : 상품 이미지  
- `state` : soft-delete (true=판매 중)  
- `userId` : 상품을 등록한 관리자

### 관계
- 1:N → Review (productId)
- 1:N → OrderDetail (productId)

### 특징
- 이미지 Key/S3 분리는 없고, URL만 저장  
- 관리자(User)의 id만 저장하여 소유 정보 관리  

---

# 4. Review (리뷰)

### 주요 컬럼
- `content`
- `imageUrl`
- `score` : 평점
- `userId` : 작성자
- `productId` : 리뷰 대상 상품

### 관계
- N:1 → User (userId)
- N:1 → Product (productId)

### 특징
- 작성자 / 상품 연결을 id 기반으로 관리  
- 이미지 업로드 후 URL 업데이트 가능

---

# 5. Orders (주문)

### 주요 컬럼
- `state` : 주문 상태 (Enum)  
  (`PENDING`, `PAID`, `SHIPPING`, `COMPLETED`, `CANCELED` 등)
- `userId` : 주문자
- `addressId` : 배송 주소
- `kakaoTid` : 결제 트랜잭션 ID

### 관계
- N:1 → User (userId)
- N:1 → Address (addressId)
- 1:N → OrderDetail (orderId)

### 특징
- 결제 시 카카오 API를 통해 TID 저장  
- 주문 상태 변경 로직 포함

---

# 6. OrderDetail (주문 상세)

### 주요 컬럼
- `orderId` : 주문 번호
- `productId`
- `productName` : 주문 당시 상품명 스냅샷
- `price` : 주문 당시 상품 가격 스냅샷
- `quantity`
- `reviewed` : 리뷰 작성 여부

### 관계
- N:1 → Orders (orderId)
- N:1 → Product (productId)

### 특징
- 주문 당시의 상품 가격/이름을 **스냅샷으로 저장**  
- 리뷰 작성 여부(reviewed) 플래그로 UX 제어 가능  

---

# ERD 설계 특징 요약

### 1. 완전한 ID 기반 관계
- `@ManyToOne`, `@OneToMany` 없음  
- 도메인 간 결합도를 최소화한 구조  
- MSA 전환 시에도 리스크가 적음

### 2. 스냅샷 기반 주문 구조
- OrderDetail에 상품명/가격 저장  
- 가격 변동이 있어도 이전 주문 데이터 변형 없음

### 3. Soft Delete 적용(Product)
- state=false 로 상품 비활성화

### 4. 리뷰 & 주문 상세 연계 강화
- reviewed 플래그로 "리뷰 작성 가능 여부" 제어

---