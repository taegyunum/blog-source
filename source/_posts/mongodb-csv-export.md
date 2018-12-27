---
title: mongodb csv export
date: '2018-03-06 13:25:00'
category: 'mongodb'
---

mongodb 내의 collection을 csv 파일로 export 하는 방법은 다음과 같다.

`mongoexport --db {DB 명} --collection {Collection 명} --type=csv --fieldFile {필드 파일} --out {저장 경로}`

CSV로 export 하는 경우 별도의 txt 파일로 필드명을 명시해줘야한다.

예를들면

```
name
country
tel
```
와 같은 형식으로 필드명을 txt 파일로 저장한다.

사용 실 예시는 다음과 같다.

mongoexport --db sample-database --collection users --type=csv --fieldFile fields.txt --out /tmp/users.csv


DB 내용이 한글인 경우 해당 CSV 파일을 엑셀에서 열면 글자가 깨질 수도 있다.
이 경우 구글 스프레드시트에서 문서를 열어서 xlsx 파일로 저장하면 파일을 올바르게 열 수 있다.
