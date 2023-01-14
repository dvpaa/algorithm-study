## 문제

https://www.acmicpc.net/problem/14500


## 풀이

### 설명

정사각형의 변과 변이 이어진 도형이라는 점에서 DFS를 사용하여 풀 수 있겠다고 생각했다.

한 시작 지점에서 상,하,좌,우로 움직일 수 있고, 4개를 확인하고 return하면 모든 경우를 탐색하고 최댓값을 얻을 수 있다고 판단하고 코드를 작성했다.

그러나 ㅓ,ㅏ,ㅗ, ㅜ 모양은 DFS로 탐색할 수 없다는 것을 코드를 작성하고 깨달았다.

다른 방법을 생각하다가 그냥 해당 부분만 탐색하는 함수를 작성하였다. 


### 코드

```python
N, M = map(int, input().split())
graph = [list(map(int, input().split())) for _ in range(N)]
visited = [[False] * M for _ in range(N)]

dx = [-1, 1, 0, 0]  # up, down, left, right on x
dy = [0, 0, -1, 1]  # up, down, left, right on y
result = 0


def dfs(x, y, sum_val, cnt):
    global result

    sub_result = sum_val + graph[x][y]
    if cnt == 4:
        result = max(result, sub_result)
        return

    for i in range(3):
        nx = x + dx[i]
        ny = y + dy[i]
        if 0 <= nx < N and 0 <= ny < M:
            if not visited[nx][ny]:
                visited[nx][ny] = True
                dfs(nx, ny, sub_result, cnt + 1)
                visited[nx][ny] = False


def none_dfs(x, y):
    global result
    for i in range(4):
        sum_val = graph[x][y]
        for j in range(3):
            direction = (i+j) % 4
            nx = x + dx[direction]
            ny = y + dy[direction]

            if not (0 <= nx < N and 0 <= ny < M):
                break
            sum_val += graph[nx][ny]

        result = max(result, sum_val)


for i in range(N):
    for j in range(M):
        visited[i][j] = True
        dfs(i, j, 0, 1)
        visited[i][j] = False

        none_dfs(i, j)

print(result)
```
