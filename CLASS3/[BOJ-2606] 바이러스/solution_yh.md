## BOJ 2606 바이러스
#### 문제 접근 전략
연결되어 있는 노드의 수만 구해주면 되는 문제이다.  
DFS를 구현할 필요는 없어보인다.
##### 첫번째 풀이 - 정답
visited는 bool 타입이기 때문에 sum을 이용하여 한 번에 계산해주었다.
```python
from collections import deque

n = int(input())
graph = [[] for _ in range(n+1)]
visited = [False]*(n+1)

for _ in range(int(input())):
    s, e = map(int, input().split())
    graph[s].append(e)
    graph[e].append(s)

def bfs(start):
    q = deque([start])
    while q:
        tmp = q.popleft()
        for n in graph[tmp]:
            if not visited[n]: 
                q.append(n)
                visited[n] = True

bfs(1)
print(sum(visited)-1)
```

##### 두번째 풀이 - 7달 전
전체적인 풀이는 똑같고 카운트를 언제해주냐의 차이이다.
```python
from collections import deque
n = int(input())
m = int(input())
info = [[] for _ in range(n+1)]
for _ in range(m):
    u, v = map(int, input().split())
    info[u].append(v)
    info[v].append(u)

visited = [False] * (n+1)
def bfs(start, count):
    queue = deque([start])
    visited[start] = True
    while queue:
        v = queue.popleft()
        for j in info[v]:
            if not visited[j]:
                queue.append(j)
                visited[j] = True
                count += 1
    return count
count = bfs(1, 0)
print(count)
```

#### 개선할 점 & 얻은 점
그래프 문제를 복습하는데에 좋은 문제였다.  
함수 이름, 변수 이름을 통일하는데에 집중하자.