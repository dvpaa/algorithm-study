## GROUP BY 유형

#### 문제 접근 전략
NAME을 그룹으로 묶어 개수를 세면 될 것 같다.

##### 첫번째 풀이 - 참고
```sql
SELECT NAME, count(*) as "COUNT"
FROM ANIMAL_INS
GROUP BY NAME
HAVING COUNT >= 2
ORDER BY NAME
```

#### 개선할 점 & 얻은 점
GRUOP BY의 조건절은 HAVING을 사용한다는 것을 다시 알아차릴 수 있었다.  
COUNT가 2개 이상인 NAME 그룹에 대해서 조건을 HAVING COUNT를 통해 주었다.