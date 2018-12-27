---
title: Ovirt DB read 권한 부여
date: 2018-05-15 16:04:55
categories: 'Ovirt'
tags:
---
Ovirt의 Database는 Postgresql을 사용합니다. Ovirt의 database는 2개가 생성되는데 engine과 ovirt_engine_history (DWH)의 read 권한을 부여하도록 하겠습니다.

engine 서버 쉘에서
```
su - postgres
scl enable rh-postgresql95 bash

psql -U postgres -c "CREATE ROLE {USERNAME} WITH LOGIN ENCRYPTED PASSWORD '{PASSWORD}';" -d ovirt_engine_history
psql -U postgres -c "GRANT CONNECT ON DATABASE ovirt_engine_history TO {USERNAME};"
psql -U postgres -c "GRANT USAGE ON SCHEMA public TO {USERNAME};" ovirt_engine_history
psql -U postgres -c "SELECT 'GRANT SELECT ON ' || relname || ' TO {USERNAME};' FROM pg_class JOIN pg_namespace ON pg_namespace.oid = pg_class.relnamespace WHERE nspname = 'public' AND relkind IN ('r', 'v');" --pset=tuples_only=on  ovirt_engine_history > grant.sql

psql -U postgres -f grant.sql ovirt_engine_history
```

engine database에 대해서도 동일한 방법으로 적용합니다.

`/var/opt/rh/rh-postgresql95/lib/pgsql/data/pg_hba.conf` 파일에 postgresql 접속을 허용하는 호스트를 입력합니다.
```
host  all  all 0.0.0.0/0 md5 (모든 대역 허용)
```

```
scl enable rh-postgresql95 bash
systemctl restart rh-postgresql95-postgresql
```





