## BOJ 9019 DSLR

#### 문제 접근 전략
BFS를 활용한 문제이다. 로직을 잘 구현하여야 시간초과가 나지 않을 것으로 보인다.
##### 첫번째 풀이 - 시간초과
계속해서 최적화를 진행하였지만, 시간초과가 났다. 로직은 문제가 없고 재방문도 고려하기 때문에 다른 곳에서 문제가 있을 것이라고 생각하였다.
```python
import sys
from collections import deque
input = sys.stdin.readline

def get_dn(n):
    d4 = n%10
    d3 = (n//10)%10
    d2 = (n//100)%10
    d1 = (n//1000)
    return d1, d2, d3, d4

def D(n):
    n = n * 2
    if n > 9999:
        n = n % 10000
    return n
def S(n):
    n = n - 1
    if n == -1:
        n = 9999
    return n
def L(n):
    d1, d2, d3, d4 = map(str, get_dn(n))
    n = "".join([d2, d3, d4, d1])
    return int(n)
def R(n):
    d1, d2, d3, d4 = map(str, get_dn(n))
    n = "".join([d4, d1, d2, d3])
    return int(n)
def bfs(n, B):
    q = deque([])
    visited = [False]*10000
    q.append((n, ""))
    visited[n] = True
    while q:
        now, oper = q.popleft()
        if now == B:
            return oper
        d = D(now)
        s = S(now)
        l = L(now)
        r = R(now)

        if not visited[d]:
            q.append((d, oper+"D"))
            visited[d] = True
        if not visited[s]:
            q.append((s, oper+"S"))
            visited[s] = True
        if not visited[l]:
            q.append((l, oper+"L"))
            visited[l] = True
        if not visited[r]:
            q.append((r, oper+"R"))
            visited[r] = True

for _ in range(int(input())):
    A, B = map(int, input().split())
    print(bfs(A, B))
```
##### 두번째 풀이 - 정답
bfs로직에는 문제가 없었다. 그러나 L과 R을 실행 시에 불필요한 연산이 수반되었던 것이 문제였다.  
함수를 수정해 준 후 제출을 해보니 바로 정답처리가 되었다. 아래 코드는 함수를 제거한 개선 코드이다.  
pypy3 기준 5324ms로 통과하였다. 파이썬으로 통과한 코드도 있다는데 참고하면 좋을 것 같다.  
https://www.acmicpc.net/source/59336597
```python
import sys
from collections import deque
input = sys.stdin.readline
def bfs(n, B):
    q = deque([])
    visited = [False]*10000
    q.append((n, ""))
    visited[n] = True
    while q:
        now, oper = q.popleft()
        if now == B:
            return oper
        d = (2*now)%10000
        s = now-1 if now!=0 else 9999
        l = (now%1000)*10 + now//1000
        r = (now%10)*1000 + now//10

        if not visited[d]:
            q.append((d, oper+"D"))
            visited[d] = True
        if not visited[s]:
            q.append((s, oper+"S"))
            visited[s] = True
        if not visited[l]:
            q.append((l, oper+"L"))
            visited[l] = True
        if not visited[r]:
            q.append((r, oper+"R"))
            visited[r] = True

for _ in range(int(input())):
    A, B = map(int, input().split())
    print(bfs(A, B))
```
##### 개선할 점 & 얻은 점
bfs를 활용한 문제 중에 가장 오래 걸렸던 문제였다. 최적화를 하는 부분에서 시간이 굉장히 오래걸렸다.  
십진수를 이용한 테크닉에서 위와 같은 방법도 사용될 수 있다는 것을 배웠다.