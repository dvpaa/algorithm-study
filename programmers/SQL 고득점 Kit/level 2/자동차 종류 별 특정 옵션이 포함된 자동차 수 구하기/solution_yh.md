## GROUP BY 유형

#### 문제 접근 전략


##### 첫번째 풀이 - 참고
```sql
SELECT CAR_TYPE, COUNT(*) as CARS
FROM CAR_RENTAL_COMPANY_CAR
WHERE OPTIONS LIKE "%통풍시트%" or OPTIONS LIKE "%열선시트%" or OPTIONS LIKE "%가죽시트%"
GROUP BY CAR_TYPE
ORDER BY CAR_TYPE
```

#### 개선할 점 & 얻은 점
