---
title: "KVM, Kimchi 설치"
date: 2018-02-27 16:30:00
category: 'Virtual Machine'
---

Centos 7에 KVM 설치 후 Kimchi 와 연동해서 제어할 수 있도록 구축하려한다.

# 호스트 설치

## 설치 준비

- KVM 모듈 설치유무 확인 `lsmod | grep kvm`
- 가상화 지원유무 확인 `egrep '(vmx|svm)' --color=always /proc/cpuinfo`
- Selinux 해제
	```
	vi /etc/selinux/config

	SELINUX=disabled

	#설정 후 재부팅
	```
- EPEL REPO 추가 `yum install epel-release`
- 불필요한 Software 방화벽 해제 `systemctl stop firewalld`
- Kimchi 서버의 경우 8001 포트 오픈

## 설치
- `yum install kvm libvirt qemu-kvm`
- 설치 확인 `lsmod | grep kvm`

## 네트워크 설정

- `yum install bridge-utils`
- br0 어댑터 생성
	```
	vi /etc/sysconfig/network-scripts/ifcfg-br0

	DEVICE=br0
	NM_CONTROLLED=no
	ONBOOT=yes
	TYPE=Bridge
	BOOTPROTO=none
	IPADDR=192.168.0.171    ### 해당값 입력
	GREFIX=24
	GATEWAY=192.168.0.1     ### 해당값 입력
	DNS1=168.126.63.1		 
	DNS2=168.126.63.2
	NAME="System br0" 

	```

- eth0 네트워크 수정

	```
	vi /etc/sysconfig/network-scripts/ifcfg-eth0

	## 기존 내용 모두 삭제 후 아래 라인만 추가

	BRIDGE=br0

	```

- 네트워크 재시작 `/etc/init.d/network restart`

- 네트워크 설정 확인 `ifconfig`


# Kimchi 설치

## 설치준비 
(위와 동일)

## Dependency 설치

- `sudo yum install gcc make autoconf automake gettext-devel git rpm-build \
                    libxslt`

- `sudo yum install libvirt-python libvirt libvirt-daemon-config-network \
                    qemu-kvm python-ethtool sos python-ipaddr nfs-utils \
                    iscsi-initiator-utils pyparted python-libguestfs \
                    libguestfs-tools novnc spice-html5 \
                    python-configobj python-magic python-paramiko \
                    python-pillow`

- `sudo yum install python-ordereddict`

- libvirt 재시작 `systemctl restart libvirtd`


## RPM 설치

- `wget https://github.com/kimchi-project/kimchi/releases/download/2.5.0/kimchi-2.5.0-0.el7.centos.noarch.rpm`
- `wget https://github.com/kimchi-project/kimchi/releases/download/2.5.0/wok-2.5.0-0.el7.centos.noarch.rpm`

- `yum install <wok.rpm> <kimchi.rpm>`


## 서비스 시작

- `systemctl start wokd`


## 서비스 접속

- `https://<machine-ip>:8001`



