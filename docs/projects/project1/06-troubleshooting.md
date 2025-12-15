---
title : 트러블 슈팅
---
# 트러블 슈팅

## 동시성 제어
- 1차 트러블 슈팅
    - 1차 문제 상황 (**락을 걸어도 결제 이후 수량 업데이트 문제 )**
        - 주문 처리 중에 락을 걸었지만, 결제가 완료된 이후에 상품 수량이 업데이트되어 수량이 1개인 상품이라도 주문서가 여러 개 생성될 수 있습니다.
        - 락을 걸어놨지만 결제가 완료된 시점에서 수량이 업데이트 되기 때문에 수량이 1개라고 해도 주문서가 100개가 생길 수가 있다.
        - a와 b의 주문서가 생기고 a와 b 둘 다 결제창에 진입한다. 둘 다 결제가 진행 된 후에 수량이 1개만 줄어들 위험이 있다.
        - 지금은 결제 모듈로 카카오 API를 사용하고 있는데 다른 결제 모듈들을 가지고 왔을때 그 모듈들에도 락을 걸어줘야 한다.
    - 1차 해결 방안
        - 분산 락을 적용할 정확한 시점을 고민해보고 주문하기에 락을 걸어서 동시성을 제어 했다.
    - 1차 해결 방안 효과
        - 주문하기 자체에 락을 걸어서 재고가 1일 때 A,B가 동시에 주문해도 한 명만 결제가 될 수 있도록 개선했다.
        - 100명 1000명이 시도해도 재고가 10개면 10개만 받고 깔끔하게 10명만 결제하기로 넘어갈 수 있다.
- 2차 트러블 슈팅
    - 2차 문제 상황
        - 개선된 코드에서 발생한 문제
        - 수량이 100개인 상품을 어떤 유저 한명이 100개를 주문해놓고 결제를 안하면 다른사람이 결제를 할 수가 없다. ex) 주문량 빌런
    - 2차 해결 방안
        - 스케줄링을 통한 문제 해결
        - 주문하기 버튼을 클릭하면 "5분 이내에 결제가 완료되지 않으면 주문이 자동으로 취소됩니다."라는 팝업 메시지를 표시한다. 이와 함께 스케줄링 기능을 도입하여, 주문 후 5분 이내에 결제가 이루어지지 않은 경우 해당 주문을 자동으로 취소 처리하고 주문된 수량만큼 재고를 복원한다.
    - 2차 해결 방안 효과
        - 미결제 주문으로 인한 재고 낭비와 판매 기회 손실을 최소화할 수 있게 되었다.
        - 사용자 경험 측면에서도 결제 완료에 대한 적절한 안내를 제공하고, 보다 효율적인 주문 처리 흐름을 제공할 수 있게 되었다.

* **상세 내용:** 
    - Redis를 사용한 동시성 제어 [바로가기](https://github.com/pie0902/TIL/blob/main/Spring/SpringBootPractices/redis-lock/1.Redis%EB%A5%BC_%EC%82%AC%EC%9A%A9%ED%95%9C_%EB%8F%99%EC%8B%9C%EC%84%B1_%EC%A0%9C%EC%96%B4.md)
    - 동시성 제어에서 겪은 문제 해결 과정 [바로가기](https://github.com/pie0902/TIL/blob/main/Spring/SpringBootPractices/redis-lock/2.%EB%8F%99%EC%8B%9C%EC%84%B1_%EC%A0%9C%EC%96%B4%EC%97%90%EC%84%9C_%EA%B2%AA%EC%9D%80_%EB%AC%B8%EC%A0%9C_%ED%95%B4%EA%B2%B0_%EA%B3%BC%EC%A0%95.md)
    - 동시성 문제 해결을 위한 재고 관리 전략 수정 [바로가기](https://github.com/pie0902/TIL/blob/main/Spring/SpringBootPractices/redis-lock/4.%EB%8F%99%EC%8B%9C%EC%84%B1_%EB%AC%B8%EC%A0%9C_%ED%95%B4%EA%B2%B0%EC%9D%84_%EC%9C%84%ED%95%9C_%EC%9E%AC%EA%B3%A0_%EA%B4%80%EB%A6%AC_%EC%A0%84%EB%9E%B5_%EC%88%98%EC%A0%95.md)
    - 동시성 제어와 스케줄링을 통한 효과적인 주문 및 재고 관리 전략[바로가기](https://github.com/pie0902/TIL/blob/main/Spring/SpringBootPractices/redis-lock/5.%EB%8F%99%EC%8B%9C%EC%84%B1_%EC%A0%9C%EC%96%B4%EC%99%80_%EC%8A%A4%EC%BC%80%EC%A4%84%EB%A7%81%EC%9D%84_%ED%86%B5%ED%95%9C_%ED%9A%A8%EA%B3%BC%EC%A0%81%EC%9D%B8_%EC%A3%BC%EB%AC%B8_%EB%B0%8F_%EC%9E%AC%EA%B3%A0_%EA%B4%80%EB%A6%AC_%EC%A0%84%EB%9E%B5.md)
    - 동시성 제어에서 주문 취소 통보: Amazon SES를 활용한 메일 전송 전략[바로가기](https://github.com/pie0902/TIL/blob/main/Spring/SpringBootPractices/redis-lock/6%20%EB%8F%99%EC%8B%9C%EC%84%B1_%EC%A0%9C%EC%96%B4%EC%97%90%EC%84%9C_%EC%A3%BC%EB%AC%B8_%EC%B7%A8%EC%86%8C_%ED%86%B5%EB%B3%B4%3AAmazon_SES%EB%A5%BC_%ED%99%9C%EC%9A%A9%ED%95%9C_%EB%A9%94%EC%9D%BC_%EC%A0%84%EC%86%A1_%EC%A0%84%EB%9E%B5.md)


## API GATEWAT

- 문제 상황
    - 프론트엔드에서 여러 서버에 날리는 각각의 fetch를 관리하기 힘들고 JWT 토큰 관리 코드를 각 서버마다 가지고 있는 점에서 성능 이슈를 느낌
- 해결 방안
    - 프론트엔드와 서버 사이에 API 엔드포인트를 관리하는 API GATEWAY를 생성 해당 GATEWAY에서 JWT 관련 검증을 이루고 각 서버에는 유저 정보만 넘겨주게됨.

## SWAP 메모리
<img src="/docs/img/project1/swap_memory.png" alt="MSA Architecture" />

- 문제 상황
    - EC2 프리티어를 사용 중 MSA 서버 5개를 docker-compose를 이용하니 cpu 및 메모리 문제로 서버가 다운되었다.
- 1차 해결 방안
    - (프리티어 t2.micro 메모리 1기가) 인스턴스를 재시작하여 확인해보았지만 저장소 문제로 파일수정등에 문제가 생겨 저장소(볼륨)을 8GiB에서 프리티어 상한선 30GiB로 설정하여 여유 공간을 확보하고 CPU메모리의 문제를 해결
- 2차 해결 방안 (1차 해결 이후 같은 현상 발생)
    - 스왑 메모리를 사용하여 4기가정도를 스왑메모리로 설정해주었다. 다행이 인스턴스의 사양을 높이지 않고 해결을 할 수 있었습니다. 하지만 스왑 메모리의 단점들이 존재 하기 떄문에 지속적으로 확인하여 성능에 영향이 간다고 판단되면 인스턴스의 사양을 높이기로 하였다

## 쿼리 개선
- 문제 상황
    - MSA 사이에서 Feign 통신 혹은 DB에 접근하는 쿼리가 N+1 문제가 발생하여 잦은 통신과 많은 쿼리가 생성되는 문제가 발생했다.
- 해결 방안
    - 쿼리나 Feign 수를 줄이기 위한 join을 활용한 쿼리 최적화를 통해 해결했습니다. 이를 통해 쿼리의 수를 줄이고 Feign통신 횟수도 감소하였습니다.
* **배치 조회 전략 ver** 
    - 배치 조회 전략 을 사용한 쿼리 개선과정 [바로가기](https://github.com/pie0902/TIL/blob/main/Spring/SpringBootPractices/MSA%ED%99%98%EA%B2%9D%EC%97%90%EC%84%9C_%EB%B0%B0%EC%B9%98_%EC%A1%B0%ED%9A%8C_%EC%A0%84%EB%9E%B5%EC%9D%84_%ED%86%B5%ED%95%9C_%EC%BF%BC%EB%A6%AC_%EA%B0%9C%EC%84%AC.md)
