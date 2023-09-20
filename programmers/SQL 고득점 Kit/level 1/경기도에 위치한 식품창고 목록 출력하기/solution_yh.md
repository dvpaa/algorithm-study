## IS NULL 유형

#### 문제 접근 전략
null 값인 경우 'N'으로 대체하여 출력하면 되는 문제

##### 첫번째 풀이 - 참고
```sql
SELECT WAREHOUSE_ID, WAREHOUSE_NAME, ADDRESS, IFNULL(FREEZER_YN, 'N') as FREEZER_YN
FROM FOOD_WAREHOUSE
WHERE WAREHOUSE_NAME LIKE '%경기%'
ORDER BY WAREHOUSE_ID
```

#### 개선할 점 & 얻은 점
IFNULL 함수를 사용하여 IFNULL(column_name, replacement_value) 형식으로 지정해주면 결측값이 대체 값으로 바뀐다