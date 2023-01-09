## 문제
https://www.acmicpc.net/problem/9095


## 풀이
### 설명
처음엔 dp로 접근하여 바텀업 방식으로 생각해보았다.

그러나 점화식이 쉽게 안 떠올라 dfs와 메모이제이션을 사용하여 풀었다.

### 코드
```python
import sys

input = sys.stdin.readline


def dfs(i):
    global n
    if i > n:
        return

    dp[i] += 1
    for j in range(1, 4):
        dfs(i + j)


for _ in range(int(input())):
    n = int(input())
    dp = [0] * (n + 1)
    dfs(0)
    print(dp[n])
```


문제를 다 풀고 다른 사람들의 풀이를 보니 dp풀었다. 점화식은 dp[i] = dp[i-1] + dp[i-2] + dp[i-3] 이다.

계산과정에서 실수를 하기도 했고, 5이상부터는 직관적으로 떠오르지도 않았다.

또한 결정적으로 1112 와 1121을 어떻게 구분해야 할지 감이 잡히지 않아서  dp로의 접근을 포기했었는데, 좀 더 생각하는 힘을 길러야곘다.
