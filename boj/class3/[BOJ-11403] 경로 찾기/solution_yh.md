## BOJ 11403 경로 찾기

#### 문제 접근 전략
dfs를 이용하여 depth를 타고 들어가 방문한 곳마다 1로 처리해주면 된다.  
또는 플로이드워셜을 이용해서 거쳐갈 수 있는 경우라면 1로 처리해주는 방식도 있다.
##### 첫번째 풀이 - 정답
DFS를 이용하여 방문한 곳이라면 1로 바꾸어주었다.
```python
n = int(input())
dp = [[0]*n for _ in range(n)]
graph = [[] for _ in range(n)]
for i in range(n):
    tmp = list(map(int, input().split()))
    for j in range(n):
        if tmp[j]:
            graph[i].append(j)

def dfs(n, visited):
    for i in graph[n]:
        if not visited[i]:
            visited[i] = True
            dfs(i, visited)

for i in range(n):
    visited = [False] * (n)
    dfs(i, visited)
    for j in range(n):
        if visited[j]:
            dp[i][j] = 1

for i in range(n):
    print(*dp[i])
```
##### 두번째 풀이 - 정답
플로이드 워셜을 이용해 모든 경로에 대해서 거쳐가는 경우가 있다면 1로 변환해주는 방식이다.  
O(n^3)의 시간복잡도가 구현되기에 더 오래걸린다.
```python
n = int(input())
graph = [list(map(int, input().split())) for _ in range(n)]

for k in range(n):
    for i in range(n):
        for j in range(n):
            if graph[i][k] and graph[k][j]:
                graph[i][j] = 1

for g in graph:
    print(*g)
```
#### 개선할 점 & 얻은 점
전형적인 그래프 문제로 다양한 알고리즘으로 풀 수 잇는 문제였다.