## BOJ 1259 직각삼각형

#### *문제 접근 전략
쉬운 수학문제이다.  
다양한 방법이 있지만 제곱의 합이 큰변의 제곱의 두배와 같다는 것을 이용하여 풀이하였다.

##### 첫번째 풀이 - 정답
```python
while True:
    try:
        arr = [x**2 for x in list(map(int, input().split()))]
        if arr == [0, 0, 0]: break
        print("right") if max(arr)*2 == sum(arr) else print("wrong")
    except EOFError:
        break
```

#### 개선할 점 & 얻은 점
빠르게 넘어가겠다.