---
description: 'Update : 2021-03-09'
---

# TransitGateway 구성하기

## TransitGateway 기본 구성

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

![](.gitbook/assets/image%20%281%29.png)

**앞서 다운로드 받은 yaml 파일들 중에 `Seoul-VPC-HQ.yml` 파일을 업로드 합니다.**

```text
Seoul-VPC-HQ.yml
```

![](.gitbook/assets/image%20%282%29.png)

다음을 선택하고, 아래와 같아 스택이름은 파일명과 동일하게 입력합니다. 

![](.gitbook/assets/image%20%284%29.png)

{% hint style="warning" %}
스택이름을 파일명과 다르게 입력하지 마십시요. 이후 과정에서 TransitGateway의 yaml파일은 , VPC yml 에서 생성된 값들을 import 해서 TGW를 생성합니다. 스택이름을 파일명과 다르게 할 경우, TGW를 생성할 때 에러가 발생합니다.
{% endhint %}

별도로 설정 변경없이, 다음 단계를 진행하고 , 승인을 선택하고 스택생성합니다.

![](.gitbook/assets/image%20%286%29.png)

**다운로드 받은 yaml 파일 3개를 추가로 반복적으로 수행합니다.** 

```text
Seoul-VPC-PRD.yml
Seoul-VPC-STG.yml
Seoul-VPC-DEV.yml
```

4개의 VPC가 모두 정상적으로 구성되면 아래와 같이 Cloudformation에서 확인 할 수 있습니다.  4개의 VPC는 각 3분 내외에 생성됩니다. 동시에 수행해도 가능합니다.

![](.gitbook/assets/image%20%288%29.png)

### Task2. TGW구성하기.

4개의 VPC를 연결할 TransitGateway를 Region에 Cloudformation으로 생성합니다.

![](.gitbook/assets/image.png)

다음을 선택하고, 아래와 같아 스택이름은 파일명과 동일하게 입력합니다. \(TGW는 스택이름을 다르게 지정해도, 본 랩을 구성하는데 문제가 없습니다.\)

![](.gitbook/assets/image%20%283%29.png)

5분 이내에 TransitGateway가 완성됩니다.

![](.gitbook/assets/image%20%287%29.png)

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

