## BOJ 11053 가장 긴 증가하는 부분 수열

#### 문제 접근 전략
여러 스택을 계속해서 만들면서 값을 추가해주는 방식으로 풀이하면 될 것 같다.
##### 첫번째 풀이 - 오답
스택을 이용하여 풀이하였다. 풀었을 때는 맞았다 생각해보니 WA가 나오자마자 아 당연히 아니겠구나 생각했다.
```python
from collections import deque

n = int(input())
arr = deque(list(map(int, input().split())))
stacks = [[arr.popleft()] for _ in range(n)]
while arr:
    i = 0
    now = arr.popleft()
    while True:
        if stacks[i]: # 현재 스택에 값이 존재할 때
            if stacks[i][-1] < now:
                stacks[i].append(now)
                break
            else:
                i += 1
        else:
            stacks[i].append(now)
            break

maximum = 0
for i in range(n):
    if stacks[i]:
        maximum = max(maximum, len(stacks[i]))
    else:
        break
print(maximum)
```

##### 두번째 풀이 - 다른 사람 풀이 참고
DP문제였다. dp[i]의 정의는 arr[i]를 마지막 값으로 가지는 가장 긴 부분수열의 길이이다.  
이중 for문을 통해 0~i까지 순회하며 arr[i]값이 arr[j]값보다 클 때, dp[i]은 현재 dp[i]의 값과 dp[j]에서 현재 값을 추가한 수 중 큰 값이다.
```python
n = int(input())
arr = list(map(int, input().split()))
dp = [1]*n
for i in range(1, n):
    for j in range(i):
        if arr[i] > arr[j]:
            dp[i] = max(dp[i], dp[j]+1)
print(max(dp))

```

#### 개선할 점 & 얻은 점
DP문제에 약한 것 같다. 지금까지 풀었던 문제 중 가장 많이 틀렸던 문제 유형이 DP이다. DP라는 것을 깨닫기가 쉽지 않은데 많은 문제를 풀어 봐야할 것 같다.