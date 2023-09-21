## GROUP BY 유형

#### 문제 접근 전략
group by와 date_format을 이용해서 출력하면 되는 문제이다.

##### 첫번째 풀이 - 정답
```sql
SELECT date_format(DATETIME, '%H') as HOUR, count(*) as COUNT
FROM ANIMAL_OUTS
WHERE date_format(DATETIME, '%H') >= 9 and date_format(DATETIME, '%H')<= 19
GROUP BY HOUR
ORDER BY HOUR
```

##### 두번째 풀이 - 참고
```sql
SELECT hour(DATETIME) AS HOUR, count(*) as COUNT
FROM ANIMAL_OUTS
WHERE hour(DATETIME) between 09 and 19
GROUP BY HOUR
ORDER BY HOUR
```

#### 개선할 점 & 얻은 점
sql에는 다양한 함수가 있는데 시간 관련 함수를 사용하여 쉽게 풀 수 있는 문제이다.  
HOUR함수로 datetime 형식의 데이터를 넣어주면 24시 형식의 시간만 추출해준다.  
또한 between 함수를 이용하여 간단하게 작성해줄 수 있다.