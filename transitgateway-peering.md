# TransitGateway Peering

## Transit Gateway Peering 

### 개요

Transit Gateway는 서로 다른 리전에서 동일한 Transit Gateway를 사용할 수 없습니다. 서로 다른 리전은 서로 다른 TGW를 구성해야 하고, 상호 연결을 위해서는 Transit Gateway Peering을 사용해야 합니다.

이번 챕터에서는 us-east-1 에서 VPC와 TGW를 생성하고 상호간에 연결 구성을 해 봅니다.

### 구성 아키텍쳐 소개



AWS 콘솔 창 상단 우측바에서 리전을 선택하고, "us-east-1" "버지니아 북부"를 선택합니다.

![](.gitbook/assets/image%20%2899%29.png)

#### Task 1. VPC 구성하기

**`새로운 계정에 접속`** 하고, Cloudformation을 통해 기본이 되는 VPC구성을 먼저 구성합니다.

**1.사전 준비하기**

**다운로드 받은 파일 중에 IAD-VPC.yml, IAD-TGW.yml 을 사용합니다.**

앞서 만들어 둔 keypair는 서울리전에서만 존재합니다. us-east-1 버지니아 리전에서도 사용할 수 있도록 Cloud9 콘솔 터미널에서 아래와 같이 명령을 입력하고 서울리전의 public key를 전송합니다.

```text
### Converting from private key to public key
sudo ssh-keygen -y -f ~/environment/builders20210312.pem > ~/environment/builders20210312.pub

### Transfer public key to us-east-1
cd ~/environment
aws ec2 import-key-pair --key-name builders20210312 --public-key-material fileb://builders20210312.pub --region us-east-1

```

**2.Cloudformation 생성.**

**AWS 관리콘솔 - Cloudformation 으로 이동하고, 새로운 리소스를 선택 합니다.** 

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



![](.gitbook/assets/image%20%2896%29.png)

![](.gitbook/assets/image%20%2897%29.png)

![](.gitbook/assets/image%20%28100%29.png)



```text
aws ec2 describe-instances --query 'Reservations[].Instances[].[Tags[?Key==`Name`] | [0].Value, Placement.AvailabilityZone,InstanceId, InstanceType, ImageId,State.Name, PrivateIpAddress, PublicIpAddress ]' --output table --region us-east-1

```



```text
aws ssm start-session --target "IAD-VPC-Private-10.4.21.101" --region us-east-1

```



```text
ping SEOUL-VPC-DEV-Private

```

#### 해당 LAB의 질문 사항은 whchoi98@gmail.com/ whchoi@amazon.com 또는 🙋♂ [슬랙채널](https://whchoi-hol.slack.com/archives/C01QM79Q4BD)\([https://whchoi-hol.slack.com/archives/C01QM79Q4BD](https://whchoi-hol.slack.com/archives/C01QM79Q4BD)\)에서 문의 가능합니다. 

