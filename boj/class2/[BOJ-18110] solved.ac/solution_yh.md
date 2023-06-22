## BOJ 18110 solved.ac

#### 문제 접근 전략
부동소수점을 이용한 문제이다. 반올림에 유의해서 풀이를 해야한다.  
소수점 자리가 0.5보다 크거나 같다면 1만큼 올림수, 작다면 내림수를 해주는 함수 하나를 선언해준다.

##### 첫번째 풀이 - 다른 사람 풀이 참고
```python
import sys

def my_round(val):
    return int(val) + 1 if val - int(val) >= 0.5 else int(val)

input = sys.stdin.readline
n = int(input())
if n:
    arr = [int(input()) for _ in range(n)]
    arr.sort()
    nn = my_round(n * 0.15)
    print(my_round(sum(arr[nn:-nn] if nn else arr) / (n - 2 * nn)))
else:
    print(0)
```

#### 개선할 점 & 얻은 점
부동소수점 계산 시에 많은 오류가 있었다.   
소수점 관련 문제가 나와서 반올림에 관한 문제가 발생 시에 위 함수를 적절히 사용하여 풀이하면 좋을 것 같다.