---
title: 'Error: ENOENT: no such file or directory, open platforms/android/res/values/strings.xml'
date: 2018-12-27 13:12:50
categories: ionic
---

Ionic Android 빌드 과정 중

`Error: ENOENT: no such file or directory, open 'platforms/android/res/values/strings.xml'`

의 오류가 발생할 경우

`MY_APP\plugins\cordova-plugin-firebase\scripts\after_prepare.js` 의 파일 내용 중 51번째 라인을

`stringsXml: ANDROID_DIR + '/app/src/main/res/values/strings.xml'` 과 같이 수정

** Reference**
- https://github.com/ionic-team/ionic/issues/13702#issuecomment-353971341
