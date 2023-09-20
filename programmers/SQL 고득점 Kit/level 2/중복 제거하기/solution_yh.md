## sum,max,min 유형

#### 문제 접근 전략
name 열의 고윳값을 구한 후 개수를 세면 된다.

##### 첫번째 풀이 - 참고
```sql
SELECT count(distinct NAME) as "count"
FROM ANIMAL_INS
```

#### 개선할 점 & 얻은 점
고윳값의 개수를 세는 테크닉을 배운 문제이다.