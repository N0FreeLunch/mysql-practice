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
                    ELSE 'Low Order'
            END
ORDER BY 1, 2;
```
