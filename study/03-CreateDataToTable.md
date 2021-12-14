## 데이터 넣기
- CDM 또는 powershell에서 sql_dump/ANSL_ 폴더로 이동
- sqlplus명령으로 유저 어카운트(C##ORA_SQL_TEST)로 접속
- `@SQLBooster_C1_03_데이터생성.sql`을 실행하여 데이터를 넣는다.

## 권한 문제로 테이블에 데이터를 넣지 못할 경우
- SYS AS SYSDBA으로 로그인
```
GRANT CREATE ANY TABLE TO C##ORA_SQL_TEST
```
```
GRANT CONNECT, RESOURCE, DBA TO C##ORA_SQL_TEST
```

## 에러가 발생한 경우
- 테이블을 다 지우고 ""테이블 생성" -> "데이터 생성" 과정을 반복한다.
