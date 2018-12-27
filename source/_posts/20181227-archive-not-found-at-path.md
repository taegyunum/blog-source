---
title: archive not found at path
date: 2018-12-27 13:19:09
categories: ionic
---

ionic에서 iOS 빌드 과정 중
`error: archive not found at path` 와 같은 오류가 발생한 경우

CLI로 빌드 시 아래 명령어를 통해 빌드

`ionic cordova build ios -- --buildFlag="-UseModernBuildSystem=0"`

**Reference**
- https://github.com/apache/cordova-ios/issues/407#issue-360392411
