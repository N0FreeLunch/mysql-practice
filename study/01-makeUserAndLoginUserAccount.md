## table space란?
[Document](https://docs.oracle.com/cd/B19306_01/server.102/b14200/statements_7003.htm)

## create user
### Oracle version 12 or later
```
CREATE USER C##ORA_SQL_TEST
IDENTIFIED BY "1qaz2wsx"
DEFAULT TABLESPACE ORA_SQL_TEST_TS;
```

### Oracle version 11
```
CREATE USER ORA_SQL_TEST
IDENTIFIED BY "1qaz2wsx"
DEFAULT TABLESPACE ORA_SQL_TEST_TS;
```

## change user default tablespace
### check user db
```
desc dba_users;
```
### check user default tablespace
```
select DEFAULT_TABLESPACE from dba_users where USERNAME='C##ORA_SQL_TEST';
```
### change user default tablespace
```
ALTER USER C##ORA_SQL_TEST DEFAULT TABLESPACE ORA_SQL_TEST_TS;
```


## admit login authority
```
ALTER USER C##ORA_SQL_TEST ACCOUNT UNLOCK;
GRANT CONNECT, RESOURCE TO C##ORA_SQL_TEST;
```

## grant authority
(Root account)
```
GRANT ALTER SYSTEM TO C##ORA_SQL_TEST;
GRANT SELECT ON V_$SQL TO C##ORA_SQL_TEST;
GRANT SELECT ON V_$SQL_PLAN_STATISTICS_ALL TO C##ORA_SQL_TEST;
GRANT SELECT ON V_$SQL_PLAN TO C##ORA_SQL_TEST;
GRANT SELECT ON V_$SESSION TO C##ORA_SQL_TEST;
GRANT EXECUTE ON DBMS_STATS TO C##ORA_SQL_TEST;
GRANT SELECT ON DBA_SEGMENTS TO C##ORA_SQL_TEST;
```

## set temp file size
```
SELECT T1.FILE_NAME
        ,(T1.BYTES/1024/1024) TMP_MB
FROM DBA_TEMP_FILES T1;
```
### change temp file size
```
ALTER DATABASE TEMPFILE 'C:\DEV\18.0.0\ORADATA\XE\TEMP01.DBF'
RESIZE 5000M;
```

## login
```
username : C##ORA_SQL_TEST
password : 1qaz2wsx
```
