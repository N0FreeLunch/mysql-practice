## create user
### Oracle version 12 or later
```sql
CREATE USER C##ORA_SQL_TEST IDENTIFIED BY "1qaz2wsx" DEFAULT TABLESPACE ORA_SQL_TEST_TS;
```

### Oracle version 11
```sql
CREATE USER ORA_SQL_TEST IDENTIFIED BY "1qaz2wsx" DEFAULT TABLESPACE ORA_SQL_TEST_TS;
```

## 디폴트 테이블 스페이스 변경
### check user db
```sql
desc dba_users;
```
### check user default tablespace
```sql
select DEFAULT_TABLESPACE from dba_users where USERNAME='C##ORA_SQL_TEST';
```
#### 테이블 스페이스란?
- 데이터베이스 오브젝트 내 실제 데이터를 저장하는 물리적인 공간
- 데이터를 저장할 물리적 위치를 지정할 뿐이며 논리적 데이터 베이스나 스키마를 지정하지 않는다.

### change user default tablespace
```sql
ALTER USER C##ORA_SQL_TEST DEFAULT TABLESPACE ORA_SQL_TEST_TS;
```
- 특정 유저가 사용할 디폴트 테이블 스페이스를 지정


## admit login authority
(Root account)
```sql
ALTER USER C##ORA_SQL_TEST ACCOUNT UNLOCK;
```
- 계정을 새로 만들거나 30일 이상 쓰지 않았을 경우 오라클 디비는 자동으로 계정을 잠그므로 계정이 락되어 있다면 언락을 해 줘야 한다.

```sql
GRANT CONNECT, RESOURCE TO C##ORA_SQL_TEST;
```
- CONNECT : ALTER SESSION, CREATE CLUSTER, CREATE DATABASE LINK, CREATE SEQUENCE, CREATE SESSION, CREATE SYNONYM
, CREATE TABLE, CREATE VIEW
- RESOURCE : CREATE CLUSTER, CREATE INDEXTYPE, CREATE OPERATOR, CREATE PROCEDURE, CREATE SEQUENCE, CREATE TABLE, CREATE TRIGGER, CREATE TYPE
- 여러 권한을 합쳐놓은 그룹 단위로 역할(ROLE)을 부여하는 것.


## grant authority
(Root account)
```sql
GRANT ALTER SYSTEM TO C##ORA_SQL_TEST;
```
- 멀티 테넌트 컨테이너 데이터베이스(CDB)와 플러그형 데이터베이스(PDB)를 변경할 수 있다.
- https://docs.oracle.com/database/121/SQLRF/statements_2017.htm#SQLRF00902

```sql
GRANT SELECT ON V_$SQL TO C##ORA_SQL_TEST;
```
```sql
GRANT SELECT ON V_$SQL_PLAN_STATISTICS_ALL TO C##ORA_SQL_TEST;
```
```sql
GRANT SELECT ON V_$SQL_PLAN TO C##ORA_SQL_TEST;
```
```sql
GRANT SELECT ON V_$SESSION TO C##ORA_SQL_TEST;
```
```sql
GRANT EXECUTE ON DBMS_STATS TO C##ORA_SQL_TEST;
```
```sql
GRANT SELECT ON DBA_SEGMENTS TO C##ORA_SQL_TEST;
```

## set temp file size
```sql
SELECT T1.FILE_NAME
        ,(T1.BYTES/1024/1024) TMP_MB
FROM DBA_TEMP_FILES T1;
```

### change temp file size
```sql
ALTER DATABASE TEMPFILE 'C:\DEV\18.0.0\ORADATA\XE\TEMP01.DBF' RESIZE 5000M;
```

## login
- username : C##ORA_SQL_TEST
- password : 1qaz2wsx

---

## 용어

### 멀티테넌트
- Oracle Multitenant를 사용하면 Oracle Database가 컨테이너 데이터베이스(CDB) 역할을 하도록 할 수 있습니다.
- CDB란? 스키마, 스키마 객체 및 비 스키마 객체로 이루어진 이식 가능한 컬렉션인 플러그형 데이터베이스(PDB)를 여러 개 통합한 것입니다.
- Oracle Multitenant에서는 온프레미스에 배포되든 클라우드에 배포되든 관계 없이 애플리케이션이 자체 포함된 PDB에서 변경 없이 실행되기 때문에 리소스 활용도, 관리 및 전반적인 보안이 향상됩니다.

- Reference : https://www.oracle.com/kr/database/multitenant/
