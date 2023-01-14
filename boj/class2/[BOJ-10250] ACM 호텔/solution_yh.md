## BOJ 10250 ACM 호텔

#### *문제 접근 전략
열을 기준으로 손님이 한 명씩 차는 구조.  
무조건 낮은 호수가 좋기 때문에 행의 개수만큼 계속 반복해주는 방법을 이용.  

##### 첫번째 풀이 - 정답
좋은 풀이라고는 생각되지 않는다.  
난이도에 비해 생각보다 고전했던 문제였다.  
나머지와 몫을 이용하여 문제를 풀어보았으나 답이 잘 나오지 않아  
우선 직관적인 방법을 사용하여 풀이를 하였다.
```python
def check(a, b, n):
    cnt = 1
    for i in range(b):
        room = i+1
        for j in range(a):
            room += 100
            if cnt >= n:
                return room
            cnt += 1

for _ in range(int(input())):
    h, w, n = map(int, input().split())
    result = check(h, w, n)
    print(str(result))
```

##### 두번째 풀이 - 다른사람 코드 참고
층수에 100을 곱하고 호수를 더하면 쉽게 문자열에 대한 에러를 해결할 수 있는 것을 확인.  
너무 문자열로 접근을 하려했다보니 호수 구하는 부분에서 오류가 있었음.  
```python
for _ in range(int(input())):
    h, w, n = map(int, input().split())
    if n%h==0:
        floor = h
        room = n//h
    else: 
        floor = n%h
        room = n//h+1
    print(str(floor*100+room))
```
#### 개선할 점 & 얻은 점
다양한 풀이가 문제를 보는 시야를 길러주는 거라고 직접 느껴보자.