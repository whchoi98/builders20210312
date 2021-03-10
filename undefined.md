---
description: 'Update : 2021-03-10'
---

# 사전 준비

## 사전 준비 사항 및 도구 소개 

* **키 페어**
* **Cloud9 구성**
* **System Manager & Session Manager \(랩에서 Cloudformation으로 자동배포 합니다.\)** 

랩 시작에 앞서 다음과 같은 사전 준비를 합니다.

모든 EC2 인스턴스 콘솔은 Cloud9 또는 Session Manager를 통해서 접속합니다. 따라서 Cloud9과 System Manager - Session Manager가 반드시 필요합니다.

System Manager와 Session Manager는 Cloudformation 기반의 Yaml을 통해 모두 사전 구성되어 있습니다.

Cloud9은 비용이 별도로 부과되지 않은 Cloud 기반의 IDE 콘솔 도구 입니다.

## 키 페어 만들기

**`AWS 관리 콘솔 - EC2 - 네트워크 및 보안 - 키 페어- 키페어 생성` 을 선택합니다.**

![](.gitbook/assets/image%20%2881%29.png)

![](.gitbook/assets/image%20%2884%29.png)

**아래와 같이 키페어 이름을 입력합니다. 해당 키 페어는 이름을 동일하게 합니다.**

```text
builders20210312
```

**파일 형식을 `pem`을 선택하고, `키 페어 생성` 을 클릭합니다.**

![](.gitbook/assets/image%20%2882%29.png)

**생성되면 pem key를 로컬 PC에 다운 받습니다**. \(저장 경로는 각 운영체제의 기본 다운로드 폴더 입니다.\)

![](.gitbook/assets/image%20%2885%29.png)

**`AWS 관리 콘솔 - EC2 - 네트워크 및 보안 - 키 페어` 을 선택하고 정상적으로 만들어 졌는지 확인합니다.**

![](.gitbook/assets/image%20%2880%29.png)

{% hint style="info" %}
해당 키페어 이름은 다음 실습에서 Cloudformation에 이미 binding 되어 있습니다. 다르게 할 경우에는 Cloudformation 진행과정에서 다시 선택해도 됩니다.
{% endhint %}

## Cloud9 구성







