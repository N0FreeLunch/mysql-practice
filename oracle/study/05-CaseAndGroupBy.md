P.34

```sql
SELECT T1.ORD_ST
    ,CASE	WHEN	T1.ORD_AMT	>=	5000	THEN	'High Order'
            WHEN	T1.ORD_AMT	>=	3000	THEN	'Middle Order'
            ELSE    'Low Order'
    END     ORD_AMT_TP
    ,COUNT(*) ORD_CNT
FROM    T_ORD T1
GROUP BY    T1.ORD_ST
        ,CASE	WHEN	T1.ORD_AMT	>=	5000	THEN	'High Order'
                WHEN	T1.ORD_AMT	>=	3000	THEN	'Middle Order'
                ELSE    'Low Order'
        END
ORDER BY 1, 2;
```

## 주문이란 무엇인가?
- 주문은 상품에 대한 신청 단위를 의미한다.

## 쿼리 설명
- 주문(T_ORD) 테이블에서 하나의 레코드는 하나의 주문을 의미한다.
- 주문(T_ORD) 테이블에서 주문상태(ORD_ST)를 표시하고, 단일 주문의 양(ORD_AMT) 5000 이상인 대상은 High Order로 표기하며, 단일 주문의 양(ORD_AMT)이 3000 이상인 대상은 Middle Order로 표기를 하며, 단일 주문의 양(ORD_AMT)이 3000 이하인 주문은 Low Order로 표기한다.
- 각 그룹별 총 갯수를 ORD_CNT으로 표기한다.
- 주문(T_ORD) 테이블에 대해서 주문상태(ORD_ST)와 '단일 주문 총량에 대한 문자표기'를 GROUP BY 한다.
- GROUP BY로 인해서 주문상태(ORD_ST)와 '단일 주문 총량에 대한 문자표기'를 조합으로 리스트 내의 유니크한 레코드를 형성한다.
- 주문의 총 갯수(ORD_CNT)는 GROUP BY로 묶인 레코드의 총 갯수를 의미한다.

#### 단일 주문 총량에 대한 문자표기
```
,CASE	WHEN	T1.ORD_AMT	>=	5000	THEN	'High Order'
        WHEN	T1.ORD_AMT	>=	3000	THEN	'Middle Order'
        ELSE 'Low Order'
END
```

#### 주문의 총 갯수와 '단일 주문 총량에 대한 문자표기'
- 주문이라는 것은 데이터베이스의 표현으로는 주문 테이블의 단일 레코드를 형성하는 대상이다.
- 주문의 갯수라는 것은 형성된 주문 레코드의 총 갯수를 의미한다.
- 단일 주문의 총량이라는 것은 주문 테이블의 하나의 레코드에 기록된 주문 량(ORD_AMT) 컬럼 데이터의 양을 의미한다.

### GROUP BY 대상은 GROUP BY 이전과 이후의 VALUE가 동일해야 한다.
- GROUP BY의 '단일 주문 총량에 대한 문자표기'를 보면 테이블의 컬럼만을 대상으로 사용하지 않았다. SELECT 절의 표기 대상과 동일한 표기를 사용한 것이고 이는 GROUP BY가 GROUP BY절을 사용하기 전에 표현되는 리스트(집계 함수 사용을 제외한 쿼리 결과)를 대상으로 작동하는 것임을 드러낸다.
- GROUP BY 이후의 표현되는 레코드와 GROUP BY 이전의 표현되는 레코드가 1:N의 관계를 가질 때 이 레코드를 비교하면, GROUP BY의 대상이 되는 값은 GROUP BY 이전과 GROUP BY 이후의 레코드가 동일한 VALUE를 가져야 한다. 이는 표현될 수 있는 결과를 기준으로 GROUP BY를 한다는 것을 의미한다.


### CASE
- CASE는 여러 개의 레코드의 데이터 표현을 일정 묶음 단위로 표현할 수 있게 만들어 준다.
- GROUP BY는 GROUP BY 이전과 이후의 동일 VALUE 값을 대상으로 하기 때문에 CASE와 같은 여러 데이터를 하나의 단위로 묶는 표현을 사용했을 때 GROUP BY도 사용할 수 있다.
