---
description: 'Update : 2021-03-09'
---

# TransitGateway 구성하기

## 1.TransitGateway 기본 구성

### 구성 아키텍쳐 소개

AWS TransitGateway의 기본 동작 이해를 위해, 가장 기본이 되는 디자인을 먼저 구성해 봅니다.

아래 그림은 이번 Chapter에서 구성해 볼 아키텍쳐 입니다. 

### Task1. VPC 구성하기

Cloudformation을 통해 기본이 되는 VPC구성을 먼저 구성합니다. 

#### 1.사전 준비하기 

서울 리전에 4개의 VPC를 구성하고, 사전에 구성된 TGW를 배포합니다.

아래 Github에서 실습에 사용할 Cloudformation yaml 파일을 다운로드 받습니다.

```text
git clone https://github.com/whchoi98/builders20210312
```

#### 2.Cloudformation 생성.

Seoul-VPC-HQ, Seoul-VPC-PRD, Seoul-VPC-STG, Seoul-VPC-DEV를 Cloudformation 을 기반으로 생성합니다.

**AWS 콘솔에서 서울 리전 \(ap-northeast-2\)를 선택하고, Cloudformation 서비스를 선택합니다.**

**Cloudformation에서 먼저 새로운 스택을 생성합니다.**

![](.gitbook/assets/image%20%285%29.png)

**앞서 다운로드 받은 yaml 파일들 중에 `Seoul-VPC-HQ.yml` 파일을 업로드 합니다.**

```text
Seoul-VPC-HQ.yml
```

![](.gitbook/assets/image%20%286%29.png)

다음을 선택하고, 아래와 같아 스택이름은 파일명과 동일하게 입력합니다. 

![](.gitbook/assets/image%20%2811%29.png)

{% hint style="warning" %}
스택이름을 파일명과 다르게 입력하지 마십시요. 이후 과정에서 TransitGateway의 yaml파일은 , VPC yml 에서 생성된 값들을 import 해서 TGW를 생성합니다. 스택이름을 파일명과 다르게 할 경우, TGW를 생성할 때 에러가 발생합니다.
{% endhint %}

별도로 설정 변경없이, 다음 단계를 진행하고 , 승인을 선택하고 스택생성합니다.

![](.gitbook/assets/image%20%2818%29.png)

**다운로드 받은 yaml 파일 3개를 추가로 반복적으로 수행합니다.** 

```text
Seoul-VPC-PRD.yml
Seoul-VPC-STG.yml
Seoul-VPC-DEV.yml
```

4개의 VPC가 모두 정상적으로 구성되면 아래와 같이 Cloudformation에서 확인 할 수 있습니다.  4개의 VPC는 각 3분 내외에 생성됩니다. 동시에 수행해도 가능합니다.

![](.gitbook/assets/image%20%281%29.png)

### Task2. TGW구성하기.

4개의 VPC를 연결할 TransitGateway를 Region에 Cloudformation으로 생성합니다.

![](.gitbook/assets/image.png)

다음을 선택하고, 아래와 같아 스택이름은 파일명과 동일하게 입력합니다. \(TGW는 스택이름을 다르게 지정해도, 본 랩을 구성하는데 문제가 없습니다.\)

![](.gitbook/assets/image%20%2810%29.png)

5분 이내에 TransitGateway가 완성됩니다.

![](.gitbook/assets/image%20%283%29.png)

## 2.TransitGateway 구성 확인

### Task1.TGW 구성 확인 

AWS 관리콘솔 - VPC 를 선택합니다.

4개의 VPC가 정상적으로 생성되었는지 확인합니다.

![](.gitbook/assets/image%20%2821%29.png)

AWS 관리콘솔 - EC2를 선택합니다.

EC2가 정상적으로 생성되었는지 확인합니다.

![](.gitbook/assets/image%20%2830%29.png)

VPC - TransitGateway를 선택해서, Transit Gateway 정상적으로 구성되었는지 확인합니다.

![](.gitbook/assets/image%20%282%29.png)

![](.gitbook/assets/image%20%2812%29.png)

### Task2. TGW Attachment 확인. 

#### `VPC-Transit Gateway-Transit Gateway 연결` 을 선택해서, Transit Gateway attachment가 정상적으로 구성되었는지 확인합니다.

![](.gitbook/assets/image%20%2815%29.png)

Seoul-TGW-Attach-Seoul-VPC-HQ를 선택하면, 이미 "Seoul-VPC-HQ"의 TGW-Subnet ID에 연결되어 있는 것을 확인할 수 있습니다. 또한 Routing Table에 Association 된 상태도 확인이 가능합니다.

1. **TGW Routing Table과 Attachment가 연결된 상태를 확인**
2. **Attachment가 VPC의 어떤 Subnet과 연결되었는지 확인** 

![](.gitbook/assets/image%20%2820%29.png)

 아래에서 나머지 VPC들도 선택해서 확인해 봅니다. 

```text
Seoul-TGW-Attach-Seoul-VPC-STG
Seoul-TGW-Attach-Seoul-VPC-DEV
Seoul-TGW-Attach-Seoul-VPC-PRD
```

### Task3. TGW Routing Table 확인. 

**`VPC-Transit Gateway-Transit Gateway- Transit Gateway 라우팅 테이블`** 을 선택해서 라우팅 테이블 구성을 확인해 봅니다. 라우팅 테이블은 2개로 구성되어 있습니다.

East-To-West 트래픽을 위한 라우팅 테이블 도메인, North-To-South 트래픽을 위한 라우팅 테이블 도메인으로 구성되어 있습니다. Seoul-VPC-HQ 는 North-To-South 라우팅 테이블 도메인에 속해 있습니다.

**먼저 North-To-South 라우팅 테이블 도메인을 확인합니다.**

**해당 라우팅 테이블 도에인에는 Seoul-VPC-HQ만 허용됩니다.**

![](.gitbook/assets/image%20%2813%29.png)

Propagation 탭을 눌러서, Seoul-VPC-HQ 테이블이 업데이트 되었는지 확인합니다.

![](.gitbook/assets/image%20%289%29.png)

North-To-South 라우팅 테이블의 Routes를 선택해서 Static Route 를 확인합니다. Seoul-VPC-HQ는 이미 앞서 propagate되어 있기 때문에 자동으로 테이블에 업데이트 되어 있습니다.

0.0.0.0/0이 목적지인 트래픽은 모두 Seoul-VPC-HQ로 향하게 구성되어 있으며, 이것은 기본값이 아니고, Cloudformation yaml에서 선언한 것입니다. 다음 단원에서 Seoul-VPC-PRD의 인스턴스들이 , Seoul-VPC-HQ를 통해서 외부에 접속하도록 하기 위해서 설정되었습니다.

**East-To-West Routing Table 도메인을 선택하여, 라우팅 테이블 속성을 확인합니다.**

해당 라우팅테이블 도메인에는 Seoul-VPC-PRD, Seoul-VPC-STG, Seoul-VPC-DEV만 연결되어 있습니다.

![](.gitbook/assets/image%20%287%29.png)

Routing Propagations를 선택해서, 모든 라우팅 테이블을 포함하고 있는지 확인합니다. 연결에는 Seoul-VPC-HQ가 없지만, 다른 라우팅 테이블 도메인에 포함되어 있습니다. 라우팅 테이블을 East-To-West에도 포함 시킨 것을 확인 할 수 있습니다.

![](.gitbook/assets/image%20%2826%29.png)

East-To-West 라우팅 테이블의 Routes를 선택해서 Propogation 된 테이블들이 정상적으로 구성되었는지 확인합니다.

![](.gitbook/assets/image%20%284%29.png)

## 3. TGW 기반 트래픽 제어

Task1. Production VPC 인터넷 제어

Production VPC는 이미 IGW와 NAT Gateway가 포함되어 있습니다. Production VPC의 Private Subnet에 배치되어 있는 EC2 인스턴스를 Transit Gateway로 경유해서 Seoul-VPC-HQ의 NATGW를 통해 사용하도록 합니다.









Task2.

#### Windows Session manager plugin 설치

```text
https://s3.amazonaws.com/session-manager-downloads/plugin/latest/windows/SessionManagerPluginSetup.exe
```

#### Mac OS용 Session manager plugin 설치

번들 설치 관리자를 다운로드합니다.

```text
curl "https://s3.amazonaws.com/session-manager-downloads/plugin/latest/mac/sessionmanager-bundle.zip" -o "sessionmanager-bundle.zip"
```

패키지의 압축을 풉니다.

```text
unzip sessionmanager-bundle.zip
```

설치 명령을 실행합니다.

```text
sudo ./sessionmanager-bundle/install -i /usr/local/sessionmanagerplugin -b /usr/local/bin/session-manager-plugin
```

Fedora Linux 에서 Session Manager Plugin 설치

```text
curl "https://s3.amazonaws.com/session-manager-downloads/plugin/latest/linux_64bit/session-manager-plugin.rpm" -o "session-manager-plugin.rpm"
sudo yum install -y session-manager-plugin.rpm
```

Ubuntu에서 Session Manager Plugin 설치

```text
curl "https://s3.amazonaws.com/session-manager-downloads/plugin/latest/ubuntu_64bit/session-manager-plugin.deb" -o "session-manager-plugin.deb"
sudo dpkg -i session-manager-plugin.deb
```

