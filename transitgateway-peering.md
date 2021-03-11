---
description: 'Update: 2021-03-09'
---

# TransitGateway Peering

## 1.Transit Gateway Peering 

### 개요

Transit Gateway는 서로 다른 리전에서 동일한 Transit Gateway를 사용할 수 없습니다. 서로 다른 리전은 서로 다른 TGW를 구성해야 하고, 상호 연결을 위해서는 Transit Gateway Peering을 사용해야 합니다.

이번 챕터에서는 us-east-1 에서 VPC와 TGW를 생성하고 상호간에 연결 구성을 해 봅니다.

### 구성 아키텍쳐 소개

AWS 관리 콘솔 창 상단 우측바에서 리전을 선택하고, **`"us-east-1" "버지니아 북부"`**를 선택합니다.

![](.gitbook/assets/image%20%2899%29.png)



## 2. EC2,VPC,TGW 구성 

### Task 1. VPC 구성하기

**`새로운 리전(버지니아 북부 us-east-1 접속`** 하고, Cloudformation을 통해 기본이 되는 VPC구성을 먼저 구성합니다.

**사전 준비하기**

앞서 서울 리전에서 만들어 둔 keypair \(public key\)는 서울리전에서만 존재합니다. 

us-east-1 버지니아 리전에서도 사용할 수 있도록 Cloud9 콘솔 터미널에서 아래와 같이 명령을 입력하고 서울리전의 public key를 전송합니다.

```text
### Converting from private key to public key
sudo ssh-keygen -y -f ~/environment/builders20210312.pem > ~/environment/builders20210312.pub

### Transfer public key to us-east-1
cd ~/environment
aws ec2 import-key-pair --key-name builders20210312 --public-key-material fileb://builders20210312.pub --region us-east-1

```

정상적으로 public key가 us-east-1 리전 Keypair에 전송되었는지 확인합니다.

**`AWS 관리 콘솔 - EC2 - 네트워크 및 보안 - 키페어`** 를 클릭하고, **`builders20210321`**  이라는 Public key가 전송되었는지 확인합니다. 

![](.gitbook/assets/image%20%28104%29.png)

**2.Cloudformation 에서 생성.**

**AWS 관리콘솔 - Cloudformation 으로 이동하고, 새로운 리소스를 선택 합니다.** 

**다운로드 받은 파일 중에 IAD-VPC.yml, IAD-TGW.yml 을 사용합니다.**

**`IAD-VPC`** 를 Cloudformation 을 기반으로 생성합니다.

![](.gitbook/assets/image%20%2895%29.png)

다운로드 받아 둔 파일 중에서 IAD-VPC.yml 파일을 업로드하고, 다음을 선택합니다. 

![](.gitbook/assets/image%20%28102%29.png)

다음을 선택하고, 아래와 같아 스택이름은 파일명과 동일하게 입력합니다.

```text
IAD-VPC
```

![](.gitbook/assets/image%20%2898%29.png)

별도로 설정 변경없이, 다음 단계를 진행하고 , 승인을 선택하고 스택생성합니다.

![](.gitbook/assets/image%20%28103%29.png)

정상적으로 구성되면 아래와 같이 Cloudformation에서 확인 할 수 있습니다. VPC는 각 3분 내외에 생성됩니다.

![](.gitbook/assets/image%20%28101%29.png)

### Task2. TGW구성하기.

IAD-VPC를 연결할 TransitGateway를 버지니아 리전\(us-east-1\)에 Cloudformation으로 생성합니다. 다운로드 받은 파일 중에 , **`IAD-TGW.yml`** 파일을 업로드 합니다.

![](.gitbook/assets/image%20%2896%29.png)

다음을 선택하고, 아래와 같아 스택이름은 파일명과 동일하게 입력합니다. \(TGW는 스택이름을 다르게 지정해도, 본 랩을 구성하는데 문제가 없습니다.\)

![](.gitbook/assets/image%20%2897%29.png)

5분 이내에 TransitGateway가 완성됩니다.

![](.gitbook/assets/image%20%28100%29.png)

### Task3. VPC, EC2 구성 확인하기.

**`AWS 관리콘솔 - VPC`** 를 선택합니다.

VPC가 정상적으로 생성되었는지 확인합니다.

![](.gitbook/assets/image%20%28107%29.png)

AWS 관리콘솔 - EC2를 선택합니다.

EC2가 정상적으로 생성되었는지 확인합니다.

![](.gitbook/assets/image%20%28111%29.png)

### Task 4. TGW 구성 확인

**`AWS 관리콘솔 - VPC - TransitGateway`** 를 선택해서, Transit Gateway 정상적으로 구성되었는지 확인합니다.

![](.gitbook/assets/image%20%28112%29.png)

![](.gitbook/assets/image%20%28106%29.png)

### Task5. TGW Attachment 확인.

**`VPC-Transit Gateway-Transit Gateway 연결` 을 선택해서, Transit Gateway attachment가 정상적으로 구성되었는지 확인합니다.**

![](.gitbook/assets/image%20%28109%29.png)

IAD-TGW-Attach-IAD-VPC를 선택하면, 이미 "IAD-VPC"의 TGW-Subnet ID에 연결되어 있는 것을 확인할 수 있습니다. 또한 Routing Table에 Association 된 상태도 확인이 가능합니다.

1. **TGW Routing Table과 Attachment가 연결된 상태를 확인**
2. **Attachment가 VPC의 어떤 Subnet과 연결되었는지 확인**

### Task6. TGW Routing Table 확인.

**`VPC-Transit Gateway-Transit Gateway- Transit Gateway 라우팅 테이블`** 을 선택해서 라우팅 테이블 구성을 확인해 봅니다. Associations와 Propagation 탭을 눌러서, IAD-VPC 연결과 IAD-VPC의 CIDR가 정상적으로 업데이트 되었는지 확인합니다.

![](.gitbook/assets/image%20%28110%29.png)

![](.gitbook/assets/image%20%28108%29.png)

propagation이 정상적으로 구성되었기 때문에 Route 탭을 선택하면, Route Type은 Propagated 되었다고 표기됩니다.

![](.gitbook/assets/image%20%28105%29.png)

**Cloudformation을 통해서 모두 정상적으로 구성되었습니다.** 👏 

## 3. TGW Peering 구성

### Task7. SSM 에서 인스턴스 확인

모든 랩의 구성 시험은 Private 인스턴스로 시험합니다. Cloudformation을 통해 System Manager와 Session Manager를 사용할 수 있도록 자동 배포 구성하였습니다.

Session Manager를 사용할 수 있도록 아래 같이 각 PC환경에 맞추어서 AWS Session Manager Plugin을 설치합니다. Cloud9을 사용하거나 웹콘솔에서 Session Manager를 사용하면 각 PC환경에서 설치할 필요가 없습니다.

Cloud9 터미널에서 아래 aws cli 명령을 실행하여 생성된 us-east-1의 EC2 인스턴스를 확인합니다.

```text
aws ec2 describe-instances --query 'Reservations[].Instances[].[Tags[?Key==`Name`] | [0].Value, Placement.AvailabilityZone,InstanceId, InstanceType, ImageId,State.Name, PrivateIpAddress, PublicIpAddress ]' --output table --region us-east-1

```

실행한 예제입니다.

```text
whchoi:~/environment $ aws ec2 describe-instances --query 'Reservations[].Instances[].[Tags[?Key==`Name`] | [0].Value, Placement.AvailabilityZone,InstanceId, InstanceType, ImageId,State.Name, PrivateIpAddress, PublicIpAddress ]' --output table --region us-east-1
------------------------------------------------------------------------------------------------------------------------------------------------------
|                                                                  DescribeInstances                                                                 |
+-----------------------------+-------------+----------------------+-----------+------------------------+----------+---------------+-----------------+
|  IAD-VPC-Public-10.5.11.101 |  us-east-1a |  i-035c11cb024b274da |  t3.micro |  ami-038f1ca1bd58a5790 |  running |  10.5.11.101  |  44.192.97.166  |
|  IAD-VPC-Private-10.5.21.101|  us-east-1a |  i-00587949de79e0ad4 |  t3.micro |  ami-038f1ca1bd58a5790 |  running |  10.5.21.101  |  None           |
+-----------------------------+-------------+----------------------+-----------+------------------------+----------+---------------+-----------------+
```

ssm plugin을 통해서 인스턴스 ID 기반으로, 직접 Private Instance에 접속합니다.아래와 같은 명령을 통해서 직접 Private Instance에 접속합니다.

* **IAD-VPC-Private-10.5.21.101**

```text
aws ssm start-session --target "IAD-VPC-Private-10.5.21.101" --region us-east-1

```

Cloud9에서 터미널 창을 1개를 추가로 오픈하고, 아래와 같이 각 6개의 호스트에 명령을 입력하여, bash 콘솔로 접속하고, 시험할 호스트들을 host file에 등록합니다.

```text
sudo -s
echo 10.0.21.101 SEOUL-VPC-HQ-Private >> /etc/hosts 
echo 10.1.21.101 SEOUL-VPC-PRD-Private >> /etc/hosts
echo 10.2.21.101 SEOUL-VPC-STG-Private >> /etc/hosts
echo 10.3.21.101 SEOUL-VPC-DEV-Private >> /etc/hosts
echo 10.4.21.101 SEOUL-VPC-PRT-Private >> /etc/hosts
echo 10.5.21.101 IAD-VPC-Private >> /etc/hosts

```

#### Task8. 시나리오 이해하기

**1.빌더스 컴퍼니는 아래와 같은 VPC를 2개의 리전에 소유하고 있습니다.**

* **IT Control Tower : Seoul-VPC-HQ**
* **Production Workload : Seoul-VPC-PRD**
* **Staging Workload : Seoul-VPC-STG**
* **Dev Workload : Seoul-VPC-Dev**
* **Dev Workload: IAD-VPC**

**2.미국의 개발인력들이 STG,DEV,PRD 간의 잦은 네트워크 연결이 필요합니다.**

**3. 미국의 개발인력들은 한국의 리전의 인터넷을 사용하지는 않을 것입니다.**

**목표 구성과 필요작업은 아래와 같습니다.**

\*\*\*\*

#### 해당 LAB의 질문 사항은 whchoi98@gmail.com/ whchoi@amazon.com 또는 🙋♂ [슬랙채널](https://whchoi-hol.slack.com/archives/C01QM79Q4BD)\([https://whchoi-hol.slack.com/archives/C01QM79Q4BD](https://whchoi-hol.slack.com/archives/C01QM79Q4BD)\)에서 문의 가능합니다. 

