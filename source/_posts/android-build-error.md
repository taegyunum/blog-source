---
title: Cordova Android build 시 오류 발생 
date: '2018-03-26 16:23:00'
category: 'ionic'
---

Ionic 2 개발중 android build 진행 시 아래와 같은 오류가 발생했습니다.

`'Error: more than one library with package name ‘com.google.android.gms.license’.`

최근 google api 가 12버전대로 업데이트 되면서 호환에 문제가 생긴 것으로 보입니다.

cordova 기반의 하이브리드 앱 개발자 분들은 직접 project.properties 내용을 11버전대로 수정을 하거나
cordova-google-api-version 이라는 플러그인을 활용하시면 손쉽게 API 버전을 수정할 수 있습니다.

`cordova plugin add cordova-google-api-version --variable GOOGLE_API_VERSION=11.+`

*Reference*
* https://forum.ionicframework.com/t/firebase-android-build-error-with-error-more-than-one-library-with-package-name-com-google-android-gms-license/125329
* https://github.com/facebook/react-native/issues/18479
* https://github.com/transistorsoft/cordova-google-api-version
