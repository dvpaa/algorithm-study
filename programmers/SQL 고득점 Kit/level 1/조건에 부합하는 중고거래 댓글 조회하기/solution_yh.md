## select 유형

#### 문제 접근 전략
두 테이블간 중복된 컬럼명이 다수 있는 문제이다. 잘 고려해서 풀어야할 것 같다.

##### 첫번째 풀이 - 참고
```sql
SELECT B.TITLE, B.BOARD_ID, R.REPLY_ID, R.WRITER_ID, R.CONTENTS, DATE_FORMAT(R.CREATED_DATE, '%Y-%m-%d') AS CREATED_DATE
FROM USED_GOODS_BOARD B
INNER JOIN USED_GOODS_REPLY R
ON B.BOARD_ID = R.BOARD_ID
WHERE (date(B.CREATED_DATE) between '2022-10-01' and '2022-10-31')
ORDER BY R.CREATED_DATE ASC, B.TITLE ASC
```

#### 개선할 점 & 얻은 점
DATETIME형식의 컬럼의 출력부분도 수정해주어야하는 문제이다. YyMmDd 각 대소문자는 출력형식이 다르니 참고하면 좋은 문제이다.