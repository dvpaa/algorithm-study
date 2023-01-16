## BOJ 11724
#### 문제 접근 전략
무방향(양방향)그래프의 정보를 통해서 노드들을 연결시키고,  
각 노드를 방문만 해주면 되는 쉬운 문제이다.  
또는 서로소 집합을 이용하여 풀 수도 있을 것 같다.
##### 첫번째 풀이 - 정답
서로소 집합 알고리즘을 이용하여 푼 코드이다.  
마지막에 result라는 set객체를 만든 이유는 마지막 입력 후 union 시에  
루트노드로 지정이 안되는 경우가 있기 때문에 한 번 더 find를 통해 결과값을 출력해주었다.
```python
import sys

def find(parent, x):
    if parent[x] != x:
        parent[x] = find(parent, parent[x])
    return parent[x]

def union(parent, a, b):
    a = find(parent, a)
    b = find(parent, b)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b
    
n, m = map(int, input().split())
parent = list(range(n+1))
for i in range(m):
    a, b = map(int, sys.stdin.readline().split())
    if find(parent, a) != find(parent, b):
        union(parent, a, b)

result = set()
for i in parent[1:]:
    result.add(find(parent, i))
print(len(result))
```

##### 두번째 풀이 - 정답
일반적인 풀이라고 생각한다. bfs로도 풀 수 있는 문제이다.
```python
import sys
sys.setrecursionlimit(int(1e6))
    
n, m = map(int, input().split())
graph = [[] for _ in range(n+1)]
visited = [False]*(n+1)

for _ in range(m):
    a, b = map(int, sys.stdin.readline().split())
    graph[a].append(b)
    graph[b].append(a)

def dfs(x):
    visited[x] = True
    for i in graph[x]:
        if not visited[i]:
            dfs(i)

result = 0
for i in range(1, n+1):
    if not visited[i]:
        dfs(i)
        result += 1
print(result)
```

#### 개선할 점 & 얻은 점
그래프문제이기 때문에 다양한 접근을 할 수 있었다.  
disjoint-sets 알고리즘을 오랜만에 상기시킬 수 있어서 좋은 문제였다.