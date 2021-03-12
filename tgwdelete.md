---
description: '2021-03-10'
---

# TGW 자원 삭제

앞서 만들어진 자원들을 모두 삭제 합니다.

## 1.버지니아 리전 자원 삭제

### Task1. us-east-1 Cloudformation Stack 삭제

* aws 관리콘솔 - 버지니아 북부 - Cloudformation - IAD-TGW 선택 - 삭제

![](.gitbook/assets/image%20%28150%29.png)

* aws 관리콘솔 - 버지니아 북부 - Cloudformation - IAD-VPC 선택 - 삭제

### Task2. 버지니아 리전 자원  삭제  확인

EC2, VPC, TransitGateway 자원이 모두 삭제 되었는지 확인합니다.

## 2. 서울 리전 자원 삭제

### Task1. us-east-1 Cloudformation Stack 삭제

* aws 관리콘솔 - 서 - Cloudformation - Seoul-TGW 선택 - 삭제

![](.gitbook/assets/image%20%28123%29.png)

* aws 관리콘솔 - 서울  - Cloudformation - VPC 선택 - 삭제 \(나머지 모든 VPC들 삭제\) 

### **Task2. 서울 리전  자원  삭제  확인**   

EC2, VPC, TransitGateway 자원이 모두 삭제 되었는지 확인합니다.



## 3. Cloud9 자원 삭제

aws 관리콘솔 - 서울 - Cloud9 에서 아래와 같이 생성된 Cloud9 IDE를 선택하고 삭제합니다.

![](.gitbook/assets/image%20%28134%29.png)

TransitGateway MultiAccount 랩도 실행하였다면,  해당 계정에서 Cloudformation 스택을 삭제합니다.

#### 해당 LAB의 질문 사항은 whchoi98@gmail.com/ whchoi@amazon.com 또는 🙋♂ [슬랙채널](https://whchoi-hol.slack.com/)\([https://whchoi-hol.slack.com/](https://whchoi-hol.slack.com/archives/C01QM79Q4BD) , [https://join.slack.com/t/whchoi-hol/shared\_invite/zt-necc66t1-n6pSgrVfGW1w6SLAQUTP8A](https://join.slack.com/t/whchoi-hol/shared_invite/zt-necc66t1-n6pSgrVfGW1w6SLAQUTP8A)\) \#aws-builders-adv-networking-hol 에서 문의 가능합니다.

