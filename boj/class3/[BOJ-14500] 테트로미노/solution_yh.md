## BOJ 14500 테트로미노

#### 문제 접근 전략
시간복잡도를 계산해 보았을 때 완전탐색으로 풀어도 통과할 수 있는 문제이다.  
모든 경우의 블록들을 나열하고 탐색하는 방법과 ㅗ,ㅏ,ㅜ,ㅓ를 제외한 깊이가 3인 백트래킹을 이용하면 될 것 같다.

##### 첫번째 풀이 - 81% 오답
백트래킹을 이용한 풀이이다. dfs함수 부분은 틀린 곳이 없는 것 같은데 cross 함수를 다시 정의하여 풀이 해봐야겠다.
```python
import sys
input = sys.stdin.readline

n, m = map(int, input().split())
array = [list(map(int, input().split())) for _ in range(n)]
visited = [[False]*m for _ in range(n)]

dx = [0, 0, 1, -1]
dy = [-1, 1, 0, 0]

result = 0
def dfs(x, y, depth, tmp):
    if depth == 3:
        result = max(result, tmp)
        return
    for i in range(4):
        nx = x + dx[i]
        ny = y + dy[i]
        if 0 <= nx < n and 0 <= ny < m:
            if not visited[nx][ny]:
                visited[nx][ny] = True
                dfs(nx, ny, depth+1, tmp+array[nx][ny]) # 깊이와 현재 좌표 값을 더해서 dfs
                visited[nx][ny] = False

def cross(x, y, value):
    canUse = True
    for i in range(4):
        d = [0, 1, 2, 3]
        d.remove(i)
        tmp = 0
        for j in d:
            nx = x + dx[j]
            ny = y + dy[j]
            if nx < 0 or nx >= n or ny < 0 or ny >= m:
                canUse = False
                break
            tmp += array[nx][ny]
        if canUse:
            result = max(result, tmp + value)

for i in range(n):
    for j in range(m):
        visited[i][j] = True
        dfs(i, j, 0, array[i][j])
        visited[i][j] = False
        cross(i, j, array[i][j])

print(result)
```

##### 두번째 풀이 - 정답
cross 함수 부분만 모든 경우의 수를 검사하는 로직으로 작성하였다.  
역시 cross 함수 부분이 문제였다. 확인해보니까 canUse 변수의 위치가 잘못 됐었다. 바꾸어서 제출하니까 맞았다.
```python
import sys
input = sys.stdin.readline

n, m = map(int, input().split())
array = [list(map(int, input().split())) for _ in range(n)]
visited = [[False]*m for _ in range(n)]

dx = [0, 0, 1, -1]
dy = [-1, 1, 0, 0]

result = []
def dfs(x, y, depth, tmp):
    if depth == 3:
        result.append(tmp)
        return
    for i in range(4):
        nx = x + dx[i]
        ny = y + dy[i]
        if 0 <= nx < n and 0 <= ny < m:
            if not visited[nx][ny]:
                visited[nx][ny] = True
                dfs(nx, ny, depth+1, tmp+array[nx][ny]) # 깊이와 현재 좌표 값을 더해서 dfs
                visited[nx][ny] = False

cx = [(0, -1, 0, 0), (0, -1, 1, 0), (0, 0, 1, 0), (0, 0, -1, 1)]
cy = [(0, 0, -1, 1), (0, 0, 0, 1), (0, 1, 0, -1), (0, -1, 0, 0)]
def cross(x, y):
    for i in range(4): # 가능한 4가지 블록
        tmp = 0
        canUse = True
        for j in range(4):
            nx = x + cx[i][j]
            ny = y + cy[i][j]
            if nx < 0 or nx >= n or ny < 0 or ny >= m:
                canUse = False
                break
            tmp += array[nx][ny]
        if canUse:
            result.append(tmp)

for i in range(n):
    for j in range(m):
        visited[i][j] = True
        dfs(i, j, 0, array[i][j])
        visited[i][j] = False
        cross(i, j)

print(max(result))
```

#### 개선할 점 & 얻은 점
방식이 생각이 안 나면 모든 경우의 수를 써도 될 것 같다. 그러나 코테나 대회가 아니기 때문에 최고의 효율을 뽑을 수 있는 풀이로 연습하는 것이  
좋다고 생각하여 백트래킹으로 풀이하였다.