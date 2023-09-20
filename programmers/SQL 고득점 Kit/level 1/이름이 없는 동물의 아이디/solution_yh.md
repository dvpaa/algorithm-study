## IS NULL 유형

#### 문제 접근 전략
결측값인 행을 출력하는 문제이다.

##### 첫번째 풀이 - 참고
```sql
SELECT ANIMAL_ID
FROM ANIMAL_INS
WHERE NAME IS NULL
ORDER BY ANIMAL_ID
```

#### 개선할 점 & 얻은 점
ISNULL 연산자는 WHERE 컬럼 뒤에 사용하여 해당 컬럼에 결측값인 행들만 출력하게 해준다.