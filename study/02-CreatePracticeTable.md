## 실습 데이터 다운로드
- download link : https://blog.naver.com/ryu1hwan/221525912860
- sql_sump 파일의 `SQLBooster_C1_01_DB및사용자생성.sql`, `SQLBooster_C1_01_DB및사용자생성.sql` 파일을 실행하자.

## sql 파일 import
- dump sql 파일이 있는 곳으로 이동한다.
```
cd c:\dev\db\sql-practice\sql_dump
```

### 사용자 생성 SQL을 import
- **중요** Root 유저인 `SYS AS SYSDBA`으로 접속한다.
- 01에서 설정했다면 import 할 필요가 없다. (skip)
```
@SQLBooster_C1_01_DB및사용자생성.sql
```
- 이미 같은 유저가 있어서 실행이 되지 않는다면 다음을 주석 처리한다.
```sql
-- CREATE TABLESPACE C##ORA_SQL_TEST_TS DATAFILE 'C:\dev\ORA_SQL_TEST\ORA_SQL_TEST.DBA' SIZE 10G EXTENT MANAGEMENT LOCAL SEGMENT SPACE MANAGEMENT AUTO;
```
```sql
-- CREATE USER C##ORA_SQL_TEST IDENTIFIED BY "1qaz2wsx" DEFAULT TABLESPACE C##ORA_SQL_TEST_TS;
```

## 테이블 생성 SQL을 import
- **중요** Root유저가 **아닌** `C##ORA_SQL_TEST`으로 접속한다.
```sql
@SQLBooster_C1_02_테이블생성.sql
```

- 잘못 생성 했다면
```
DROP TABLE T_ORD_DET;
DROP TABLE T_ORD;
DROP TABLE T_ITM_EVL;
DROP TABLE M_CUS;
DROP TABLE M_RGN;
DROP TABLE M_ITM_PRC_HIS;
DROP TABLE M_ITM;
DROP TABLE C_BAS_CD_DV;
DROP TABLE C_BAS_CD;
```

- 외래키 제약 때문에 지울 수 없는 경우 (지울 테이블명은 바꿔 줘야 한다.)
```sql
DROP TABLE C_BAS_CD_DV CASCADE CONSTRAINTS;
```
