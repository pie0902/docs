---
title: CI/CD
---

# CI/CD 파이프라인

## GitHub Actions 기반 자동화
- GitHub Actions를 활용하여 지속적 통합(CI) 및 기본적인 지속적 배포(CD) 과정을 자동화했습니다.
- 코드 푸시 시 자동으로 빌드, 테스트가 실행되도록 구성하여 개발 효율을 높였습니다.

## Docker 기반 빌드 및 배포
- 각 마이크로서비스를 Docker 이미지로 패키징하여 일관된 실행 환경을 유지했습니다.
- 초기에는 ECS로 배포했으나, 비용 효율성을 위해 이후 Docker Hub + EC2 단일 호스트 배포 방식으로 전환했습니다.

## 테스트 자동화
- 단위 테스트 및 주요 기능 테스트를 GitHub Actions 워크플로우에 포함하여 배포 전 기본적인 검증을 수행했습니다.

## 배포 모니터링 및 롤백 전략
- 배포 후 컨테이너 상태를 모니터링하여 오류가 감지될 경우 신속한 수동 롤백이 가능하도록 구성했습니다.

---

# CI/CD (ECS)
<img src="/docs/img/project1/cicd_ecs.png" alt="CICD_ECS" style="width: 80%; max-width: 900px;" />

# CI/CD (EC2)
<img src="/docs/img/project1/cicd_ec2.png" alt="CICD_EC2" style="width: 80%; max-width: 900px;" />
