---
description: 'Update : 2021-03-09'
---

# TransitGateway 구성하기

## TransitGateway 기본 구성

### 구성 아키텍쳐 소개

AWS TransitGateway의 기본 동작 이해를 위해, 가장 기본이 되는 디자인을 먼저 구성해 봅니다.

아래 그림은 이번 Chapter에서 구성해 볼 아키텍쳐 입니다. 



### Task1. Cloudformation 구성하기

Cloudformation을 통해 기본이 되는 VPC구성을 먼저 구성합니다. 

#### 1.사전 준비하기 

서울 리전에 4개의 VPC를 구성하고, 사전에 구성된 TGW를 배포합니다.

아래 Github에서 실습에 사용할 Cloudformation yaml 파일을 다운로드 받습니다.

```text
git clone https://github.com/whchoi98/builders20210312
```

#### 2.Cloudformation 생성.

Seoul-VPC-HQ, Seoul-VPC-PRD, Seoul-VPC-STG, Seoul-VPC-DEV를 Cloudformation 을 기반으로 생성합니다.

**먼저 새로운 스택을 생성합니다.**

![](.gitbook/assets/image%20%282%29.png)

**앞서 다운로드 받은 yaml 파일들 중에 `Seoul-VPC-HQ.yml` 파일을 업로드 합니다.**

```text
Seoul-VPC-HQ.yml
```

![](.gitbook/assets/image%20%283%29.png)

![](.gitbook/assets/image%20%284%29.png)

![](.gitbook/assets/image%20%285%29.png)

**다운로드 받은 yaml 파일 3개를 추가로 반복적으로 수행합니다.** 

```text
Seoul-VPC-PRD.yml
Seoul-VPC-STG.yml
Seoul-VPC-DEV.yml
```





\*\*\*\*



