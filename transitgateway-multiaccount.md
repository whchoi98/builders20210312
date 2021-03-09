---
description: 'Update : 2021-03-09'
---

# TransitGateway MultiAccount

## Transit Gateway MultiAccount 연결 

### 구성 아키텍쳐 소개 

Transit Gateway는 동일 리전에서 서로 다른 계정에서 Transit Gateway  Peering을 사용할 수 없습니다.

예를 들어 빌더스 컴퍼니와 협력사인 서밋 컴퍼니는 상호간에 Transit Gateway Peering을 동일 리전에서 연결할 수 없습니다. 이러한 경우 RAM\(Resource Access Manager\)를 통해서 간단하게 연결할 수 있는 디자인을 제공하고 있습니다.

아래와 같이 서울 리전안에서 2개의 계정간에 개발 협력을 위해 연결하는 과정을 소개합니다.

## 서로 다른 계정에서 TGW 연동

### Task 1. VPC 구성하기

**`새로운 계정에 접속`** 하고, Cloudformation을 통해 기본이 되는 VPC구성을 먼저 구성합니다.

**1.사전 준비하기**

서울 리전에 4개의 VPC를 구성하고, 사전에 구성된 TGW를 배포합니다.

아래 Github에서 실습에 사용할 Cloudformation yaml 파일을 다운로드 받습니다. **\(이미 받았다면 생략합니다.\)**

```text
git clone https://github.com/whchoi98/builders20210312
```

**2.Cloudformation 생성.**

Seoul-VPC-PART를 Cloudformation 을 기반으로 생성합니다.

![](.gitbook/assets/image%20%2834%29.png)

**AWS 콘솔에서 서울 리전 \(ap-northeast-2\)를 선택하고, Cloudformation 서비스를 선택합니다.**

**Cloudformation에서 먼저 새로운 스택을 생성합니다.**

**앞서 다운로드 받은 yaml 파일들 중에 `Seoul-VPC-PART.yml` 파일을 업로드 합니다.**

```text
Seoul-VPC-PART.yml
```

![](.gitbook/assets/image%20%2857%29.png)

다음을 선택하고, 아래와 같아 스택이름은 파일명과 동일하게 입력합니다.

![](.gitbook/assets/image%20%281%29.png)

별도로 설정 변경없이, 다음 단계를 진행하고 , 승인을 선택하고 스택생성합니다.

![](.gitbook/assets/image%20%2845%29.png)

정상적으로 구성되면 아래와 같이 Cloudformation에서 확인 할 수 있습니다. VPC는 각 3분 내외에 생성됩니다.

![](.gitbook/assets/image%20%2812%29.png)

새로운 계정의 번호를 복사해 둡니다.

![](.gitbook/assets/image%20%2852%29.png)

### Task 2. RAM 구성하기



![](.gitbook/assets/image%20%284%29.png)

![](.gitbook/assets/image%20%2811%29.png)

![](.gitbook/assets/image%20%2839%29.png)

![](.gitbook/assets/image%20%2869%29.png)

![](.gitbook/assets/image%20%2817%29.png)

![](.gitbook/assets/image%20%2863%29.png)

![](.gitbook/assets/image%20%2840%29.png)

![](.gitbook/assets/image%20%2813%29.png)

![](.gitbook/assets/image%20%2835%29.png)

![](.gitbook/assets/image%20%2830%29.png)

![](.gitbook/assets/image%20%2877%29.png)

![](.gitbook/assets/image%20%2868%29.png)

![](.gitbook/assets/image%20%2846%29.png)

![](.gitbook/assets/image%20%2860%29.png)

![](.gitbook/assets/image%20%2856%29.png)

![](.gitbook/assets/image%20%289%29.png)

![](.gitbook/assets/image%20%2848%29.png)

### Task 3. TGW 연동하기







