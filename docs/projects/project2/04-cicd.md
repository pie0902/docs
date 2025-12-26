---
title: CI/CD
---
# CI/CD (EC2)
<img src="/docs/img/project1/cicd_ec2.png" alt="CICD_EC2" />

코드의 품질 유지와 빠른 배포를 위해 GitHub Actions를 활용한 CI/CD 파이프라인을 구축했습니다. Main 브랜치에 Push가 발생하면 자동으로 도커 이미지를 빌드하여 Docker Hub에 저장하고, 운영 서버(EC2)에서 최신 이미지를 Pull 받아 무중단 배포가 이루어지도록 자동화했습니다.

