## BOJ 14940 쉬운 최단거리

#### 문제 접근 전략
전형적인 bfs 문제이다. 좌표 간의 거리가 모두 일정한 2차원 공간에서의 한 지점에서 다른 지점의 거리는 bfs를 활용하여 최단거리를 구하면 된다.  
문제 해결을 위해 간단한 조건만 조금 추가해주면 된다.

##### 첫번째 풀이 - 정답
손코딩을 이용한 풀이다.   
다 작성하고 실행해보니 방문 처리를 해주지 않아 추가해주었다.
```python
from collections import deque
import sys
input = sys.stdin.readline

dx = [-1, 1, 0, 0]
dy = [0, 0, -1, 1]

n, m = map(int, input().split())
array = [list(map(int, input().split())) for _ in range(n)]
visited = [[False]*m for _ in range(n)]
start = (0, 0)
for i in range(n):
    for j in range(m):
        if array[i][j] == 2:
            start = (i, j)
            break

def bfs(start):
    q = deque()
    array[start[0]][start[1]] = 0
    visited[start[0]][start[1]] = True
    q.append(start)

    while q:
        x, y = q.popleft()
        for i in range(4):
            nx = x+dx[i]
            ny = y+dy[i]
            if 0<=nx<n and 0<=ny<m:
                if array[nx][ny] == 1 and not visited[nx][ny]:
                    array[nx][ny] = array[x][y] + 1
                    visited[nx][ny] = True
                    q.append((nx, ny))

bfs(start)
for i in range(n):
    for j in range(m):
        if not visited[i][j] and array[i][j] == 1:
            array[i][j] = -1

for i in range(n):
    for j in range(m):
        print(array[i][j], end=' ')
    print()
```

##### 두번째 풀이 - 정답
시작위치를 대해 리스트 컴프리헨션을 이용해서 찾아주었다.  
첫번째 풀이와 별 다른 것은 없지만 메모리, 시간이 조금 단축되었다.
```python
from collections import deque
import sys
input = sys.stdin.readline

dx = [-1, 1, 0, 0]
dy = [0, 0, -1, 1]

n, m = map(int, input().split())
array = [list(map(int, input().split())) for _ in range(n)]
visited = [[False]*m for _ in range(n)]
start = [(x, y) for x in range(n) for y in range(m) if array[x][y] == 2]

def bfs(x, y):
    q = deque()
    array[x][y] = 0
    visited[x][y] = True
    q.append((x, y))

    while q:
        x, y = q.popleft()
        for i in range(4):
            nx = x+dx[i]
            ny = y+dy[i]
            if 0<=nx<n and 0<=ny<m:
                if array[nx][ny] == 1 and not visited[nx][ny]:
                    array[nx][ny] = array[x][y] + 1
                    visited[nx][ny] = True
                    q.append((nx, ny))

bfs(start[0][0], start[0][1])
for i in range(n):
    for j in range(m):
        if not visited[i][j] and array[i][j] == 1:
            array[i][j] = -1

for i in range(n):
    for j in range(m):
        print(array[i][j], end=' ')
    print()
```

#### 개선할 점 & 얻은 점
전형적인 bfs 문제이다. 2차원 원소를 서칭하여 원하는 값의 좌표를 얻는 테크닉은 따로 존재하지 않는 것으로 확인하였다.  
순환, 리스트 컴프리헨션, enumerate를 이용하는 것 외에는 아직 찾지 못하였다.  
좌표를 찾는데에 리스트 컴프리헨션을 이용하면 간단하게 쓸 수 있다는 것은 확인하였다.