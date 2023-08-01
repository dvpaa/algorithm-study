## BOJ 11660 구간 합 구하기 5

#### 문제 접근 전략
누적합의 결과를 출력하는 횟수가 M이며 완전탐색으로 합을 구한다면 시간복잡도는 O(N*N*M)으로 시간 초과가 난다.  
그렇다면 dp를 활용하여 각 좌표까지의 누적합을 구한 후, 해당 좌표의 누적합을 메모이제이션 한 뒤, 
O(1)의 시간으로 불러오는 바텀업 방식을 활용하면 될 것 같다. 
##### 첫번째 풀이 - 오답
문제를 잘못 이해했다. (x1, y1)부터 (x2, y2)까지의 누적합이 그 사이에 있는 모든 좌표들의 누적합이 아닌 
각 좌상단, 우하단 꼭짓점으로 만들어진 직사각형 내부의 누적합이었다. 이거 때문에 시간이 굉장히 오래걸렸다.   
```python
import sys
input = sys.stdin.readline

n, m = map(int, input().split())
array = []
dp = [0]*(1024*1024)

for i in range(n):
  for j in map(int, input().split()):
    array.append(j)
dp[0] = array[0]
for i in range(1, n**2):
    dp[i] = dp[i-1] + array[i]

for i in range(m):
    a, b, c, d = map(lambda x:x-1, map(int, input().split()))
    s = a*n+b
    e = c*n+d
    print(dp[e] - dp[s] + array[s])
```

##### 두번째 풀이 - 9% 오답
행을 기준으로 구간 누적합 로직을 구현해주었다. 시간복잡도는 O(N*M)으로 파이썬으로는 시간초과가 날 것이라 예상하였다.  
python으로는 시간초과가 났고 pypy로 돌린 결과 올라가긴 했다..
```python
import sys
input = sys.stdin.readline

n, m = map(int, input().split())
array = []
dp = [0]*(1024*1024)

for i in range(n):
  for j in map(int, input().split()):
    array.append(j)
dp[0] = array[0]
for i in range(1, n**2):
    dp[i] = dp[i-1] + array[i]

for i in range(m):
    a, b, c, d = map(lambda x:x-1, map(int, input().split()))
    tmp = 0
    s, e = [], []
    for j in range(c-a+1):
        s.append(a*n+b+(j*n))
    for k in range(c-a, -1, -1):
        e.append(c*n+d-(k*n))
    for l in range(c-a+1):
        tmp += dp[e[l]] - dp[s[l]-1]
    print(tmp)
```

##### 세번째 풀이 - 정답
위 코드와 무엇이 달라졌을까? 바로 dp의 크기를 1 늘려준 것 뿐이다.  
예제와 반례 코드에서는 틀린게 없어서 계속 고민하다가, 혹시나 배열 크기가 잘못된건가? 해서 1늘려주었다.  
바로 정답; dp[0]은 array[0]번째의 누적합이고, dp[-1]은 array[-1]번째까지의 누적합이니 상관없는 거 아닌가?  
뭐가 잘못된 건지는 잘 모르겠다. 질문게시판에 올릴 예정이다.
```python
import sys
input = sys.stdin.readline

n, m = map(int, input().split())
array = []
for i in range(n):
  for j in map(int, input().split()):
    array.append(j)
dp = [0]*(1024*1024+1)      
dp[0] = array[0]
for i in range(1, n**2):
    dp[i] = dp[i-1] + array[i]

for i in range(m):
    a, b, c, d = map(lambda x:x-1, map(int, input().split()))
    tmp = 0
    s, e = [], []
    for j in range(c-a+1):
        s.append(a*n+b+(j*n))
    for k in range(c-a, -1, -1):
        e.append(c*n+d-(k*n))
    for l in range(c-a+1):
        tmp += dp[e[l]] - dp[s[l]-1]
    print(tmp)
```
#### 개선할 점 & 얻은 점
dp를 활용한 구간합 테크닉을 공부할 수 있었던 문제였다. 정말 다양한 조건을 갖는 문제가 많아 많이 풀어 보면 좋을 것 같다.  
아직도 왜 맞았는지 이해가 가지 않는다.. 