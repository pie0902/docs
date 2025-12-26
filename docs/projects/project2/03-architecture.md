---
title: architectuer
---

# architectuer


<img src="/docs/img/project2/rego-architectuer.png" alt="architectuer" />

AWS VPC 환경에서 보안을 고려하여 설계했습니다. Public Subnet에는 EC2를 배치하여 유저의 HTTP 요청을 처리하고, 데이터 유출 방지를 위해 RDS는 EC2의 보안 그룹에서 오는 3306 요청만 받도록 설정했습니다. 또한, GitHub Actions와 Docker Hub를 활용한 CI/CD 파이프라인을 구축하여 배포 자동화를 구현했습니다.