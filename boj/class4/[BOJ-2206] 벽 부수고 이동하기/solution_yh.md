## BOJ 2206 벽 부수고 이동하기

#### 문제 접근 전략
현재 벽을 부수고 왔는지 부수고 오지 않았는지에 대한 변수 하나를 추가해주어서 BFS를 돌리면 될 것 같다.

##### 첫번째 풀이 - 18% 오답
```python
from collections import deque
import sys
input = sys.stdin.readline

dx = [-1, 1, 0, 0]
dy = [0, 0, 1, -1]

n, m = map(int, input().split())
visited = [list(map(int, list(input().rstrip()))) for _ in range(n)]
block = [[False]*m for _ in range(n)]
for i in range(n):
    for j in range(m):
        if visited[i][j]:
            block[i][j] = True

def bfs(a, b, c):
    # 이전 노드가 벽을 부수고 온 노드인지 확인하기 위한 불리언 변수 추가
    q = deque([(a, b, c)])
    visited[0][0] = 1

    while q:
        x, y, canBreak = q.popleft()
        if x == n-1 and y == m-1:
            return visited[x][y]
        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]
            if nx < 0 or nx >= n or ny < 0 or ny >= m:
                continue
            if block[nx][ny] and not canBreak: # 벽이 아니면서 벽을 부수지 않은 경우
                visited[nx][ny] = visited[x][y] + 1
                q.append((nx, ny, True))  # 부순 상태로 넘겨준다
            elif not block[nx][ny] and not visited[nx][ny]:
                visited[nx][ny] = visited[x][y] + 1
                q.append((nx, ny, canBreak))  # 그대로 상태를 넘겨준다
    return -1

print(bfs((0, 0, False)))
```

##### 두번째 풀이 - 다른 사람 풀이 참고
크리티컬한 반례가 존재했다.  
만일 벽을 부수고 도착한 상황이 벽을 부수지 않고 도착한 상황보다 먼저 발생한 경우, 마지막 지점에 도달하지 못하는 경우가 있다.  
즉, 3차원 리스트를 통해서 벽을 부수고 도착한 상황과 부수지 않고 도착한 상황 2가지를 따로 저장해준다.
```python
from collections import deque
import sys
input = sys.stdin.readline

dx = [-1, 1, 0, 0]
dy = [0, 0, 1, -1]

n, m = map(int, input().split())
graph = [list(map(int, list(input().rstrip()))) for _ in range(n)]
# 3차원 리스트(행, 얄, 벽을 깬 여부)
visited = [[[0]*2 for _ in range(m)] for _ in range(n)]

def bfs(a, b, c):
    # 이전 노드가 벽을 부수고 온 노드인지 확인하기 위한 불리언 변수 추가
    q = deque([(a, b, c)])
    visited[a][b][c] = 1

    while q:
        x, y, broken = q.popleft()
        if x == n-1 and y == m-1:
            return visited[x][y][broken]
        for i in range(4):
            nx = x + dx[i]
            ny = y + dy[i]
            if nx < 0 or nx >= n or ny < 0 or ny >= m:
                continue
            # 벽을 부수면서 이동
            if graph[nx][ny] and not broken:
                visited[nx][ny][1] = visited[x][y][0] + 1 # 벽 파괴기회를 쓰지 않은 노드 + 1 => 벽 파괴 기회를 쓴 노드
                q.append((nx, ny, 1))
            # 벽이 아니며 방문하지 않은 곳
            elif not graph[nx][ny] and not visited[nx][ny][broken]:
                visited[nx][ny][broken] = visited[x][y][broken] + 1
                q.append((nx, ny, broken))
    return -1

print(bfs(0, 0, 0))
```

#### 개선할 점 & 얻은 점
간단하면서도 생각치도 못한 반례로 애를 먹은 문제이다. BFS를 3차원에서 활용하는 것이 생각보다 많이 쓰인다는 것을 다시 느낄 수 있었다.