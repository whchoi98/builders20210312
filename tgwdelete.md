---
description: '2021-03-10'
---

# TGW 자원 삭제

앞서 만들어진 자원들을 모두 삭제 합니다.

## 1.버지니아 리전 자원 삭제

### Task1. us-east-1 Cloudformation Stack 삭제

* aws 관리콘솔 - 버지니아 북부 - Cloudformation - IAD-TGW 선택 - 삭제

![](.gitbook/assets/image%20%28149%29.png)

* aws 관리콘솔 - 버지니아 북부 - Cloudformation - IAD-VPC 선택 - 삭제

### Task2. 버지니아 리전 자원  삭제  확인

EC2, VPC, TransitGateway 자원이 모두 삭제 되었는지 확인합니다.

## 2. 서울 리전 자원 삭제

### Task1. us-east-1 Cloudformation Stack 삭제

* aws 관리콘솔 - 서 - Cloudformation - Seoul-TGW 선택 - 삭제

![](.gitbook/assets/image%20%28123%29.png)

* aws 관리콘솔 - 서울  - Cloudformation - VPC 선택 - 삭제 \(나머지 모든 VPC들 삭제\) 

### **Task2. 서울 리 자원  삭제  확인**

EC2, VPC, TransitGateway 자원이 모두 삭제 되었는지 확인합니다.

