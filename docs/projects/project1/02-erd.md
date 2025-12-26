---
title: ERD
---

# ERD (Entity Relationship Diagram)

아래는 프로젝트에서 사용한 실제 엔티티 기반의 ERD입니다.

<img src="/docs/img/project1/erd.png" alt="ERD" />

---

# ERD 설계 특징 요약

- 서비스 간 통신은 Feign으로 분리
- JPA 연관관계 없이 ID(Long) 기반으로 관계 관리
- OrderDetail에 상품 정보 스냅샷 저장으로 외부 서비스 변경 영향 제거
- 리뷰 작성 가능 여부를 주문 상세(reviewed) 기준으로 제어
