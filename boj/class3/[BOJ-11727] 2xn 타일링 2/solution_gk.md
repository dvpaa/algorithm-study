## 문제
https://www.acmicpc.net/problem/11727

## 풀이
### 설명
- 전형적인 dp문제이다.
- $a_n = a_{n-1} + 2a_{n-2}$라는 점화식을 세울 수 있다.

### 코드
```python
n = int(input())
dp = [-1, 1, 3]

for i in range(3, n+1):
    dp.append((dp[i-1] + 2 * dp[i-2]) % 10007)

print(dp[n])
```
