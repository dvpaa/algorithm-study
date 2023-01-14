## BOJ 1012 유기농 배추
#### 문제 접근 전략
기초적인 bfs or dfs 문제로 상하좌우 개념이 추가되었다.  
미리 방향을 정해두고 반복문으로 탐색해주면 될 것 같다.
##### 첫번째 풀이 - 정답
배추를 지날 때 마다 0으로 만들어주었다.  
그렇게 한다면 지렁이를 부를 때 마다 결과에 1만 더해주면 된다.  
또한 방문 리스트를 따로 구현할 필요가 없다.
```python
from collections import deque
import sys

dx = [0, 0, -1, 1]
dy = [-1, 1, 0, 0]

def bfs(u, v):
    q = deque([(u, v)])
    graph[u][v] = 0
    while q:
        x, y = q.popleft()
        for i in range(4):
            nx = x+dx[i]
            ny = y+dy[i]
            if 0 <= nx < n and 0 <= ny < m:
                if graph[nx][ny] == 1:
                    q.append((nx, ny))
                    graph[nx][ny] = 0

for _ in range(int(input())):
    m, n, k = map(int, input().split())
    graph = [[0]*m for _ in range(n)]
    for _ in range(k):
        u, v = map(int, sys.stdin.readline().split())
        graph[v][u] = 1
    
    result = 0
    for x in range(n):
        for y in range(m):
            if graph[x][y] == 1:
                bfs(x, y)
                result += 1

    print(result)
```

##### 두번째 풀이 - 6달 전
쓸 데 없는 코드가 줄어들었다.
```python
# 1012
from collections import deque
import sys
input = sys.stdin.readline

dx = [-1, 1, 0, 0]
dy = [0, 0, -1, 1]

def bfs(x, y, arr):
    q = deque([(x, y)])
    if arr[x][y] == 1:
        arr[x][y] = 0
        while q:
            now_x, now_y = q.popleft()
            for i in range(4):
                nx = now_x + dx[i]
                ny = now_y + dy[i]
                if 0 <= nx <= n-1 and 0 <= ny <= m-1:
                    if arr[nx][ny] == 1:
                        q.append((nx, ny))
                        arr[nx][ny] = 0
        return True
    return False

for _ in range(int(input())):
    m, n, k = map(int, input().split())
    array = [[0] * m for _ in range(n)]
    for i in range(k):
        a, b = map(int, input().split())
        array[b][a] = 1

    result = 0
    for j in range(n):
        for k in range(m):
            if bfs(j, k, array):
                result += 1
    print(result)
```

#### 개선할 점 & 얻은 점
상하좌우 개념을 다시 한 번 상기할 수 있는 문제였다.