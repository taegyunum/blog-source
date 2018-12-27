---
title: "18/02/28 트러블슈팅 내역"
date: 2018-03-01 15:35:00
category: 'Linux'
---

트러블 슈팅 내역

## 1. 리눅스 배포판 확인

`cat /etc/*release`

-> Centos가 아닌 RHEL으로 확인됨.

## 2. Redhat Subscription 구독상태 확인

`subscription-manager version`

## 3. Redhat Subscription 미구독으로 인한 yum 사용 불가

Daum Centos Repo를 추가

`vi /etc/yum.repos.d/Daum.repo`

```
[base]

name=CentOS-$releasever - Base
baseurl=http://ftp.daum.net/centos/7/os/$basearch/
gpgcheck=1
gpgkey=http://ftp.daum.net/centos/RPM-GPG-KEY-CentOS-7

[updates]

name=CentOS-$releasever - Updates
baseurl=http://ftp.daum.net/centos/7/updates/$basearch/
gpgcheck=1
gpgkey=http://ftp.daum.net/centos/RPM-GPG-KEY-CentOS-7

[extras]

name=CentOS-$releasever - Extras
baseurl=http://ftp.daum.net/centos/7/extras/$basearch/
gpgcheck=1
gpgkey=http://ftp.daum.net/centos/RPM-GPG-KEY-CentOS-7

[centosplus]

name=CentOS-$releasever - Plus
baseurl=http://ftp.daum.net/centos/7/centosplus/$basearch/
gpgcheck=1
gpgkey=http://ftp.daum.net/centos/RPM-GPG-KEY-CentOS-7
```
## 4. 외부 인터넷 연결 불가

1) DNS 서버 설정

`vi /etc/resolv.conf`
```
nameserver 8.8.8.8
```

2) 라우팅 테이블 확인 후 누락된 라우팅 테이블 추가

`route add default gw 192.168.0.1`

3) 네트웍 재시작

`systemctl restart network`

## 5. Background 상태에 있는 프로세스 종료

1) jobs 명령어로 현재 background 상태 프로세스 들 확인

2) fg [해당 번호] 로 프로세스 전환

3) Ctrl + C 로 프로세스 종료
