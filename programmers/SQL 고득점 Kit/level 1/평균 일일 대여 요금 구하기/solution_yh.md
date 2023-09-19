## select 유형

#### 문제 접근 전략
해당 컬럼의 평균값 계산 및 반올림 함수를 사용하는 문제이다.

##### 첫번째 풀이 - 참고
```sql
SELECT round(avg(DAILY_FEE), 0) as AVERAGE_FEE
FROM CAR_RENTAL_COMPANY_CAR
WHERE CAR_TYPE = 'SUV'
```

#### 개선할 점 & 얻은 점
round 함수의 사용법을 배울 수 있는 문제이다.