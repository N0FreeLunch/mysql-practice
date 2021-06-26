# sql-practice


## Install Oracle on Windows
Version : 19 XE


## SET TABLE STORAGE
```
CREATE TABLESPACE ORA_SQL_TEST_TS DATAFILE 'C:\dev\ORA_SQL_TEST\ORA_SQL_TEST.DBA' SIZE 10G
EXTENT MANAGEMENT LOCAL SEGMENT SPACE MANAGEMENT AUTO;
```
wait a minute.


## Connection
In your windows terminal like CMD, powershell
[Reference](https://docs.oracle.com/cd/E18283_01/appdev.112/e10766/tdddg_connecting.htm#CEGDIFBC)
```
sqlplus
```

## Admin Login
[Reference](https://docs.oracle.com/database/121/ADMQS/GUID-DE8A79BD-FAE4-4364-98FF-D2BD992A06E7.htm#ADMQS0361)
```
username : SYS AS SYSDBA
```
password : 설치 시 입력한 비밀번호


## User Login
유저 계정으로 로그인 할 수 있는 설정을 먼저 해야 한다.
```
username : C##ORA_SQL_TEST
password : 1qaz2wsx
```

## Reference
```
\[Book\]
```
