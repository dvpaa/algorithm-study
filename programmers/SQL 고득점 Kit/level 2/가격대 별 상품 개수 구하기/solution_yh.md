## GROUP BY 유형

#### 문제 접근 전략
case 문과 group by를 사용하여 가격대별 개수를 구하면 될 것이다.

##### 첫번째 풀이 - 참고
```sql
SELECT 
    case 
    when price >= 0 and price < 10000 then 0
    ELSE floor(price/10000)*10000 
    END as PRICE_GROUP, 
    count(*) as PRODUCTS
FROM PRODUCT
GROUP BY PRICE_GROUP
ORDER BY PRICE_GROUP
```

#### 개선할 점 & 얻은 점
case문 사용법과 as로 바꾼 컬럼명을 뒤 명령어에서도 사용 가능하다는 것을 알았다.  
해당 문제에서는 floor함수를 통해 가격대를 구했으며, PRICE_GROUP으로 컬럼명 변경 후 GROUP BY 및 ORDER BY에 사용하였다.