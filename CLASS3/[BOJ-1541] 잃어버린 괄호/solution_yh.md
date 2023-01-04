## BOJ 1541 잃어버린 괄호
#### 문제 접근 전략
주어진 식 안에서 적절한 괄호를 쳐서 식의 최솟값을 얻는 문제이다.  
음수의 크기를 최대로 하면 최솟값이 나오므로 '-'를 기준으로 split할 것이다.  
나눠진 첫번째 문자열은 무조건 양수이기에 더해놓고 시작한다.
##### 첫번째 풀이 - 정답
문자열 안에 있는 식을 계산하는 파이썬 함수가 있었던 것으로 기억하는데 생각이 나지 않아서 우선 sum, map을 이용해주었다.
```python
s = input().split('-')
result = []
for i in s:
    result.append(sum(map(int, i.split('+'))))
print(result[0]-sum(result[1:]))
```

##### 두번째 풀이 - 6달 전
메모리, 시간, 코드길이 부분에서 아주 큰 차이가 났다.  
이중 for 문에서 내부 숫자 하나하나를 빼주는 시간이 오래 걸린 것 같다.
```python
s = input().split('-')
sum = 0
for i in s[0].split('+'):
    sum += int(i)
for i in s[1:]:
    for j in i.split('+'):
        sum -= int(j)
print(sum)
```

####