---
title: Ovirt Engine 4.2 설치 
date: '2018-03-24 22:00:00'
category: 'Ovirt'
---

# Ovirt Engine 4.2 설치

Ovirt Engine을 설치하는 방식은 Standalone 과 Self-Hosted Engine 2가지 방식이 있습니다.
HA를 구성하기 위해선 Self-Hosted Engine방식으로 구성해야합니다.
본 포스트에선 조금 더 간단한 Standalone 방식에 대해 작성하도록 하겠습니다.

## 시스템 요구사항

Ovirt-Engine의 시스템 요구사항으로

* 최소 Dual core CPU, 권장 Quad core 이상 CPU
* 최소 4GB Memory, 권장 16GB Memory
* 최소 25GB HDD, 권장 50GB 이상HDD

Ovirt를 설치하기 위해선 설치 서버에서 가상화 기능을 지원해야합니다.
해당 서버의 가상화 지원 유무는 다음 명령어를 통해 확인할 수 있습니다.
`grep -E 'svm|vmx' /proc/cpuinfo | grep nx`
위의 명령어로 조회되는 결과가 없으면 CPU에서 가상화 명령어를 지원하지 않거나, BIOS에서 가상화기능이 Off 되었을 수 있습니다.


## 방화벽 설정

Ovirt-Engine을 구동하기 위해 오픈해야하는 포트는 아래와 같습니다.

- 22 TCP
- 2222 TCP
- 80, 443 TCP
- 6100 TCP
- 7410 UDP

OS 내부의 firewalld 등의 소프트웨어를 통해 관리하는 경우 설정 과정에서 자동으로 방화벽 규칙을 세팅하도록 할 수 있습니다.
>자동으로 firewalld 규칙을 설정하도록 하는 경우 기존 방화벽 규칙을 덮어쓸 수 있습니다.

## 설치

`yum -y install http://resources.ovirt.org/pub/yum-repo/ovirt-release42.rpm`
`yum -y update`
`yum -y install ovirt-engine`

필요한 패키지의 설치가 완료되면 Ovirt-Engine 설정을 진행합니다.

`engine-setup`

설정 단계에선 특별한 경우를 제외하고 모두 기본값을 사용합니다.

설정이 완료되면 웹 브라우져에 서버 호스트명을 입력하여 관리 페이지에 접속할 수 있습니다.

초기 로그인 아이디는 admin, 비밀번호는 설정 과정에서 입력한 비밀번호로 로그인 가능합니다.
