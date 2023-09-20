## sum,max,min 유형

#### 문제 접근 전략
row를 취하는 형식이므로 이중 조건문을 사용하면 될 것이다.

##### 첫번째 풀이 - 참고
```sql
SELECT PRODUCT_ID, PRODUCT_NAME, PRODUCT_CD, CATEGORY, PRICE
FROM FOOD_PRODUCT
WHERE PRICE = (SELECT MAX(PRICE) 
              FROM FOOD_PRODUCT)
```

#### 개선할 점 & 얻은 점
단일 값이 아닌 단일 행을 구하는 문제에서 쓰이는 테크닉을 배웠다. 