## JOIN 유형

#### 문제 접근 전략
JOIN 연산을 통해 새로운 테이블 생성 후 조건에 맞게 출력하면 될 것이다.

##### 첫번째 풀이 - 정답
```sql
SELECT P.PRODUCT_CODE, sum(P.PRICE*O.SALES_AMOUNT) as SALES
FROM PRODUCT as P
INNER JOIN OFFLINE_SALE as O
ON P.PRODUCT_ID = O.PRODUCT_ID
GROUP BY P.PRODUCT_CODE
ORDER BY SALES DESC, P.PRODUCT_CODE ASC
```

#### 개선할 점 & 얻은 점
(상품 별)이므로 GROUP BY 연산을, 총 매출액 이므로 sum함수를 적용하였다.  
inner join은 product_id열을 기준으로 조인해서 풀이하였다.