## GROUP BY의 기본
```sql
SELECT T1.ORD_DT ,T1.PAY_TP
        ,SUM(T1.ORD_AMT) ORD_AMT
FROM    T_ORD T1
WHERE   T1.ORD_ST = 'COMP'
GROUP   BY T1.ORD_DT ,T1.PAY_TP
ORDER   BY T1.ORD_DT ,T1.PAY_TP;
```

### 쿼리 설명
- 주문(T_ORD) 테이블의 주문일시(ORD_DT)와 PAY_TP(지불 방법)을 표시하려고 한다.
- 이 때, 주문상태(ORD_ST)의 값이 완료(COMP)인 대상을 선택하여 보여주도록 한다.
- 이 때, 주문일시(ORD_DT)와 지불방법(PAY_TP)가 동일한 것은 묶기 위해서 GROUP BY를 사용한다.
- GROUP BY로 중복되는 항목이 단일하게 표시되도록 만들어 주었다. 따라서 '주문일시 + 지불방법'의 조합은 표시되는 리스트 내에 유일하게 존재한다.
- 주문 일시(ORD_DT)에 대해서 먼저 정렬을 하고 같은 주문일시(ORD_DT)라면 지불방법(PAY_TP)순으로 보여주도록 ORDER BY를 사용하였다.

### GROUP BY 지정 컬럼에 따른 쿼리 결과의 양상이 달라짐
- 주문일시(ORD_DT)와 지불방법(PAY_TP)이 동일한 레코드는 GROUP BY로 인해서 '주문일시 + 지불방법'의 조합이 유일하게 표시 되도록 줄여 주었다. 하지만 주문일시(ORD_DT)와 지불방법(PAY_TP) 이외의 다른 컬럼을 포함하여 GROUP BY를 했을 때는 '주문일시 + 지불방법 + 지정한 다른컬럼'의 조합이 유니크하게 표시되도록 줄여줄 경우와 다른 양상을 띈다. 왜냐하면 다른 '주문일시 + 지불방법'에 해당하는 데이터의 조합과 '주문일시 + 지불방법 + 지정한 다른컬럼'에 해당하는 데이터의 조합이 다른 레코드가 존재할 수 있기 때문이다.

### GROUP BY 이전과 이후의 관계
- 데이터 베이스의 쿼리 결과는 리스트 방식으로 구성되어 있다. GROUP BY 이전과 비교했을 때 GROUP BY로 지정한 컬럼의 조합을 유니크하게 만들기 위해 레코드 수가 줄어 든다.
- GROUP BY 이후의 리스트와 GROUP BY 이전의 리스트를 비교하면 이후의 리스트의 GROUP BY 대상 컬럼의 조합과 매칭되는 이전 리스트의 컬럼 조합은 1:N의 관계를 가진다. 이후 리스트의 하나의 컬럼에 해당하는 이전 컬럼의 레코드는 복수개 존재한다는 것.

### GROUP BY 이후 다른 컬럼의 데이터를 보고 싶을 때
- GROUP BY 절에 지정한 컬럼은 동일한데, SELECT 절에 추가적으로 컬럼을 지정하여 데이터를 보고 싶은 경우, GROUP BY 이전 리스트의 데이터를 GROUP BY 이후 리스트에 가져와서 보여주는 방식으로 이해할 수 있다. 이 때 GROUP BY 이전과 이후가 1:N의 관계를 가진다고 했는데, GROUP BY 이후의 하나의 레코드가 가질 수 있는 추가 컬럼은 N개의 값을 가지게 된다. 따라서 N개의 대상 중 무엇을 보여줄지 선택을 하든가, N개의 대상 모두를 연산한 어떤 결과를 가지는 값 하나를 보여주든 해야 한다.

### 집계함수
- GROUP BY 전 후가 GROUP BY로 지정된 컬럼 조합이 같은 레코드를 기준으로 1:N의 관계를 지닌다고 하였다. GROUP BY에 지정되지 않은 컬럼을 추가할 때 N에 대응하는 GROUP BY 이전의 리스트의 대상 레코드의 추가로 지정할 컬럼 값 모두를 연산한 어떤 결과를 가지는 값 하나를 보여주는 것이 집계함수이다.
- 집계 함수는 GROUP BY를 지정하지 않은 쿼리에도 사용할 수 있다. 이 때 연산이 되는 대상은 리스트의 지정한 컬럼 값 전체에 해당한다.

### GROUP BY가 지정되지 않은 절에 집계 함수 작성하기
```sql
SELECT  COUNT(*)            CNT
        ,SUM(T1.ORD_AMT)    TTL_ORD_AMT
        ,MIN(T1.ORD_SEQ)    MIN_ORD_SEQ
        ,MAX(T1.ORD_SEQ)    MAX_ORD_SEQ
    FROM    T_ORD T1
    WHERE   T1.ORD_DT >= TO_DATE('20170101', 'YYYYMMDD')
    AND     T1.ORD_DT < TO_DATE('20170201', 'YYYYMMDD');
```
- 위는 정상적인 SQL

```sql
SELECT T1.ORD_ST
    ,COUNT(*)           CNT
    ,SUM(T1.ORD_AMT)    TTL_ORD_AMT
    ,MIN(T1.ORD_SEQ)    MIN_ORD_SEQ
    ,MAX(T1.ORD_SEQ)    MAX_ORD_SEQ
    FROM    T_ORD T1
    WHERE   T1.ORD_DT   >=  TO_DATE('2O17O1011', 'YYYYMMDD')
    AND     T1.ORD_DT   <   TO_DATE('20170201', 'YYYYMMDD');
```
- 위는 `GROUP BY T1.ORD_ST`를 요구하는 SQL
- GROUP BY를 쓰지 않는다면, 집계 함수를 사용하지 말아야 한다.
- 집계함수를 쓴 이후의 리스트는 집계함수를 쓰기 전 리스트와 비교했을 때 전체 컬럼을 하나로 묶는 GROUP BY가 생략된 형태로 존재한다.
- GROUP BY 없이 집계함수를 쓰는 순간 GROUP BY 생략된 형태로 들어가 있는 방식이 되므로 집계함수 없이 컬럼을 표시하는 방식을 사용할 수 없다.
- 집계함수를 쓰기 전의 리스트는 하나의 레코드만 있는 리스트이며, 집계함수 이전 리스트와는 1:N이며 '1:전체'의 관계가 된다.
