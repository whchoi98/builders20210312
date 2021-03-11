---
description: 'Update : 2021-03-10'
---

# 사전 준비

## 사전 준비 사항 및 도구 소개 

* **키 페어**
* **Cloud9 구성 - EC2 인스턴스 접속과 yml 수**
* **System Manager & Session Manager \(랩에서 Cloudformation으로 자동배포 합니다.\)** 

랩 시작에 앞서 다음과 같은 사전 준비를 합니다.

모든 EC2 인스턴스 콘솔은 Cloud9 또는 Session Manager를 통해서 접속합니다. 따라서 Cloud9과 System Manager - Session Manager가 반드시 필요합니다.

System Manager와 Session Manager는 Cloudformation 기반의 Yaml을 통해 모두 사전 구성되어 있습니다.

Cloud9은 비용이 별도로 부과되지 않은 Cloud 기반의 IDE 콘솔 도구 입니다.

## 키 페어 만들기

**`AWS 관리 콘솔 - EC2 - 네트워크 및 보안 - 키 페어- 키페어 생성` 을 선택합니다.**

![](../.gitbook/assets/image%20%2882%29.png)

![](../.gitbook/assets/image%20%2888%29.png)

**아래와 같이 키페어 이름을 입력합니다. 해당 키 페어는 이름을 동일하게 합니다.**

```text
builders20210312
```

**파일 형식을 `pem`을 선택하고, `키 페어 생성` 을 클릭합니다.**

![](../.gitbook/assets/image%20%2883%29.png)

**생성되면 pem key를 로컬 PC에 다운 받습니다**. \(저장 경로는 각 운영체제의 기본 다운로드 폴더 입니다.\)

![](../.gitbook/assets/image%20%2891%29.png)

**`AWS 관리 콘솔 - EC2 - 네트워크 및 보안 - 키 페어` 을 선택하고 정상적으로 만들어 졌는지 확인합니다.**

![](../.gitbook/assets/image%20%2881%29.png)

{% hint style="info" %}
해당 키페어 이름은 다음 실습에서 Cloudformation에 이미 binding 되어 있습니다. 다르게 할 경우에는 Cloudformation 진행과정에서 다시 선택해도 됩니다.
{% endhint %}

## Cloud9 구성

### Cloud9 소개

AWS Cloud9은 브라우저만으로 코드를 작성, 실행 및 디버깅할 수 있는 클라우드 기반 IDE\(통합 개발 환경\)입니다. 코드 편집기, 디버거 및 터미널이 포함되어 있습니다. Cloud9은 JavaScript, Python, PHP를 비롯하여 널리 사용되는 프로그래밍 언어를 위한 필수 도구가 사전에 패키징되어 제공되므로, 새로운 프로젝트를 시작하기 위해 파일을 설치하거나 개발 머신을 구성할 필요가 없습니다. Cloud9 IDE는 클라우드 기반이므로, 인터넷이 연결된 머신을 사용하여 사무실, 집 또는 어디서든 프로젝트 작업을 할 수 있습니다. 또한, Cloud9은 서버리스 애플리케이션을 개발할 수 있는 원활한 환경을 제공하므로 손쉽게 서버리스 애플리케이션의 리소스를 정의하고, 디버깅하고, 로컬 실행과 원격 실행 간에 전환할 수 있습니다. Cloud9에서는 개발 환경을 팀과 신속하게 공유할 수 있으므로 프로그램을 연결하고 서로의 입력 값을 실시간으로 추적할 수 있습니다.

### 장점 소개

#### 실시간으로 함께 코딩 <a id="Code_Together_in_Real_Time"></a>

AWS Cloud9를 사용하면 코드 협업이 쉬워집니다. 클릭 몇 번으로 개발 환경을 팀과 공유하고 프로그램을 함께 연결할 수 있습니다. 협업을 진행하는 동안 팀원은 서로 입력하는 것을 실시간으로 보고 IDE 내에서 바로 채팅할 수 있습니다.

#### 손쉽게 서버리스 애플리케이션 구축 <a id="Build_Serverless_Applications_with_Ease"></a>

AWS Cloud9을 사용하면 서버리스 애플리케이션을 손쉽게 작성, 실행 및 디버깅할 수 있습니다. AWS Cloud9은 서버리스 개발에 필요한 모든 SDK, 라이브러리 및 플러그인으로 개발 환경을 사전에 구성합니다. 또한, Cloud9은 AWS Lambda 함수를 로컬에서 테스트하고 디버깅할 수 있는 환경을 제공합니다. 코드에 직접 반복할 수 있으므로 시간을 절약하고 코드 품질을 개선할 수 있습니다.

#### 터미널에서 AWS에 직접 액세스 <a id="Direct_Terminal_Access_to_AWS"></a>

AWS Cloud9에는 사전에 인증된 AWS 명령줄 인터페이스와 더불어 개발 환경을 호스팅하고 있는 관리형 Amazon EC2 인스턴스에 대한 sudo 권한이 포함된 터미널이 함께 제공됩니다. 따라서 명령을 신속하게 실행하고 AWS 서비스에 직접 액세스할 수 있습니다.

#### 새로운 프로젝트를 신속하게 시작 <a id="Start_New_Projects_Quickly_"></a>

AWS Cloud9를 사용하면 새로운 프로젝트를 손쉽게 시작할 수 있습니다. Cloud9의 개발 환경은 Node.js, JavaScript, Python, PHP, Ruby, Go 및 C++를 비롯한 40여 개의 프로그래밍 언어용 도구와 함께 사전에 패키징되어 제공됩니다. 따라서 개발 머신을 위해 파일, SDK 및 플러그인을 설치하거나 구성할 필요 없이 몇 분 만에 인기 있는 애플리케이션 스택의 코드 작성을 시작할 수 있습니다. Cloud9은 클라우드 기반이므로, 손쉽게 여러 개의 개발 환경을 유지 관리하여 프로젝트 리소스를 격리할 수 있습니다.

### Cloud9 구성

**AWS 관리 콘솔 - Cloud9**  을 선택하고, Cloud9 서비스 화면으로 이동합니다.

**Create environment** 를 선택합니다.

![](../.gitbook/assets/image%20%2886%29.png)

**Step1.** Name environment에 아래와 같이 이름을 입력하고, **Next step**을 클릭합니다. 사용자의 Cloud9은 리전당 unique 해야 합니다. 각자 영문이름을 입력하세요.

```text
mybuilders-xxxx
```

![](../.gitbook/assets/image%20%2893%29.png)

Step2. Configure settings 에서 기본값으로 사용하고, Cost-Saving setting - After four hours 를 선택합니다. 기본값은 30분이며, 30분 후에는 절전 모드로 변경됩니다. 랩에서는 4시간 동안 동작 시키도록 합니다.

![](../.gitbook/assets/image%20%2890%29.png)

{% hint style="info" %}
여기서 잠깐 !!!! Cloud9 인스턴스는 어디에 배치되나요? 

기본 Default VPC의 Public Subnet에 배치 됩니다. 만약 다른 VPC를 사전에 구성해 두었다면 변경도 가능합니다.
{% endhint %}

#### Step3. Review 단계입니다. 앞서 생성한 내용을 검토하는 단계입니다. `Create environment`를 선택합니다.

![](../.gitbook/assets/image%20%2880%29.png)

이제 2~3분 뒤면 EC2 인스턴스 기반의 Cloud IDE 생성됩니다. 

### Cloud9 둘러보기 및 환경 구성 

Cloud9은 훌륭한 Cloud IDE 환경을 제공합니다. Code 저작도구와 터미널 등을 제공하고 있기 때문에, 이 랩에서 활용해 봅니다.

환경 설정

Cloud9 화면 우측 상단의 톱니바퀴 모양 Preference 를 선택합니다.

![](../.gitbook/assets/image%20%2885%29.png)

프로젝트, User 설정, 터미널 설 등 다양한 환경을 구성할 수 있습니다. \( 이 랩에서는 자세한 소개를 생략합니다.\)

먼저 키 페어 만들기 에서 생성하고, 로컬 PC로 다운로드 받은  pem key를 Cloud9 콘솔에 업로드 합니다.

![](../.gitbook/assets/image%20%2884%29.png)

#### 정상적으로 업로드하였다면, 아래와 같이 확인 할 수 있습니다. 

![](../.gitbook/assets/image%20%2889%29.png)

#### 랩이 종료된 후에는 보안상 삭제합니다. 

**이 랩을 위해서 아래 내용을 복사해서 설치합니다.**

```text
##aws cli version 2.0 upgrade
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install

##aws cli completer
which aws_completer
export PATH=/usr/local/bin:$PATH
source ~/.bash_profile
complete -C '/usr/local/bin/aws_completer' aws

##aws ssm plugin install
curl "https://s3.amazonaws.com/session-manager-downloads/plugin/latest/linux_64bit/session-manager-plugin.rpm" -o "session-manager-plugin.rpm"
sudo yum install -y session-manager-plugin.rpm

##source download
git clone https://github.com/whchoi98/buildernet.git

```

완료 된 이후 아래와 같이 Cloud9 좌측 패널에서 yml 파일을 다운로드 받습니다. 

![](../.gitbook/assets/image%20%2894%29.png)



## 사전 준비 단계 과정 

1. **키페어 만들기 - Private Key 와 Public Key 만들고, Private Key는 안전하게 로컬 PC에 내려 받습니다.**
2. **Cloud9 만들기 - Cloud9 을 생성합니다.**
3. **Cloud9 환경 구성 - 나만의 Cloud9 환경을 꾸미고, 이번 랩에서 필요한 설정들을 구성합니다.**

* PC에 내려받은 Private key를 복사해서, 동일한 이름으로 Cloud9에 업로드
* Cloud9 터미널에 aws cli v2 설치, aws cli 자동완성 설치
* Session manager plugin 설치
* LAB에서 사용될 Cloudformation용 YAML 파일과 Shell 다운로드



#### 해당 LAB의 질문 사항은 whchoi98@gmail.com/ whchoi@amazon.com 또는 🙋♂ [슬랙채널](https://whchoi-hol.slack.com/archives/C01QM79Q4BD)\([https://whchoi-hol.slack.com/archives/C01QM79Q4BD](https://whchoi-hol.slack.com/archives/C01QM79Q4BD)\)에서 문의 가능합니다. 







