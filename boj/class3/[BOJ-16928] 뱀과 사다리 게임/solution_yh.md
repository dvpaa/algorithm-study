## BOJ 16928 뱀과 사다리 게임

#### 문제 접근 전략
전형적인 bfs 문제이다. 1차원 공간 내에서 bfs 활용 최단거리를 구하면 되는 문제이다.

##### 첫번째 풀이 - 정답
사다리나 뱀의 도착 위치에 빠르게 접근할 수 있도록 사전형을 사용하였다.  
크기가 15라서 큰 차이는 없다.
```python
from collections import deque
INF = int(1e9)

n, m = map(int, input().split())
ladder = dict()
snake = dict()

for _ in range(n):
    k, v = map(int, input().split())
    ladder[k] = v
for _ in range(m):
    k, v = map(int, input().split())
    snake[k] = v

visited = [False]*101
graph = [INF]*101
graph[1] = 0

def bfs(start):
    q = deque()
    q.append((start, 0))
    visited[start] = True
    while q:
        x, cost = q.popleft()
        if x == 100:
            return cost
        for i in range(1, 7):
            nx = x+i
            if nx <= 100 and not visited[nx]:
                if nx in ladder:
                    next_x = ladder[nx]
                    q.append((next_x, cost+1))
                elif nx in snake:
                    next_x = snake[nx]
                    q.append((next_x, cost+1))
                else:
                    q.append((nx, cost+1))
                visited[nx] = True

print(bfs(1))
```

#### 개선할 점 & 얻은 점
좌표나 노드 이동 간에 소요되는 비용이 1일 때 bfs를 활용하는 문제라는 것을 깨닫는 것이 중요하다고 다시 느꼈다.  
알고리즘 문제를 풀면서 dp로 접근하려는 습관 때문에 그래프가 생각나지 않았는데 이러한 문제점를 다시 느끼게 해주는 문제였다.