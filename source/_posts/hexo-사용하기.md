---
title: hexo 사용하기
date: 2018-05-15 14:04:22
tags: 'hexo'
---

블로그를 Hexo를 사용하여 재구성하였습니다.
한글 사용하는 것
기존 jekyll으로 구성하였을 땐 Mac OS 환경에서 Ruby 패키지 사용이 익숙치 않아 구성에 어려움이 있었습니다. 반면 Hexo는 node.js 기반으로 npm 설치를 통해 간단하게 로컬 환경을 구성할 수 있었습니다.
또한 hexo-cli 명령어를 통해 Post의 title, date, tags를 자동으로 세팅해주는 템플릿 기능이 있어 편리합니다.

## 설치
`npm install -g hexo-cli`

## 초기 설정
hexo 디렉토리 생성
`hexo init blog`
`cd blog`
`npm install`
`npm install hexo-deployer-git --save`
`npm install hexo-generator-json-content --save` (hueman 템플릿 사용시 검색 기능 활성화에 필요)

## 설정
_config.yaml
```
# Site
title: 	# 블로그명 기입
subtitle: # 블로그 부제 기입
description:  # 블로그 설명
author: # 저자
language: en 
timezone: Asia/Seoul 

# URL
url: # github page 주소

# Deployment
deploy:
  type: git
  repo: # git repo 주소 
```
## 테마 설치
블로그 설치 경로에서 아래 명령어 실행
`git clone https://github.com/ppoffice/hexo-theme-hueman.git themes/hueman`

### Hexo _config.yml 변경
설정파일 내 theme 값을 `theme: hueman` 으로 변경

## 시작
`hexo server`

## 빌드
`hexo generate`

## 배포
`hexo deploy`

## 빌드와 배포 동시에 진행
`hexo g -d`

## 포스트 작성
`hexo new post '새로운 글'`


