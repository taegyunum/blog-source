---
title : "Homebrew python3 설치 시 오류 발생"
date : 2018-03-01 16:00:00
category : 'python, mac, homebrew'
---

Mac 10.13.3 High Sierra 에서 Homebrew 를 이용하여 python3 설치 시 아래와 같은 오류가 발생하였다.

`Error: Permission denied @ dir_s_mkdir - /usr/local/Frameworks`

/usr/local/Frameworks 폴더가 존재하지 않아 발생되는 문제로 보인다.

아래의 명령어를 통해 폴더를 생성하고 올바른 퍼미션을 부여하면 문제를 해결할 수 있다.

`sudo mkdir /usr/local/Frameworks`
`sudo chown $(whoami):admin /usr/local/Frameworks`

폴더 생성 후 

`brew install python3` 또는
`brew link python3` 로 설치를 마무리한다.



*Reference* https://github.com/Homebrew/homebrew-core/issues/19286
