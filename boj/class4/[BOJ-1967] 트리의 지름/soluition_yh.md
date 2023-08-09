## BOJ 1967 트리의 지름

#### 문제 접근 전략
dfs를 활용하여 풀 수 있을 것으로 보인다. 끝 노드 간의 거리를 모두 구해주고 max값을 취하면 될 것 같다.

##### 첫번째 풀이 - 메모리 초과
노드의 수가 10000개로 메모리 초과 발생을 하였다. 그리고 해당 풀이는 O(N^2)로 어짜피 시간 초과가 날 것이라고 한다.
```python
import sys
input = sys.stdin.readline

n = int(input())
has_child = [False]*(n+1)
graph = [[] for _ in range(n+1)]
for _ in range(n-1):
    a, b, cost = map(int, input().split())
    graph[a].append((b, cost))
    # b의 부모를 a로 설정
    has_child[a] = True
    graph[b].append((a, cost))

result = []
def dfs(node, total, visited):
    # 더 이상 방문할 노드가 없을 때 해당 노드까지의 거리
    count = 0
    for i in graph[node]:
        if visited[i[0]]:
            count += 1
        else:
            visited[i[0]] = True
            dfs(i[0], total+i[1], visited)
        if count == len(graph[node]):
            result.append(total)
            return

for i in range(1, n+1):
    if not has_child[i]:
        visited = [False]*(n+1)
        visited[i] = True
        dfs(i, 0, visited)
print(max(result))

```

##### 두번째 풀이 - 다른 사람 풀이 참고
트리에서 아무 노드를 잡고 해당 노드에서 가장 먼 곳을 n1이라 했을 때,  
n1에서 가장 먼 노드를 n2라 하면, 트리의 지름은 n2-n1이 된다.  
이에 대한 증명은 여기서 확인하자. https://koosaga.com/14  
해당 로직으로 구현하면 O(N)의 시간복잡도로 풀이할 수 있다.
```python
import sys
input = sys.stdin.readline
sys.setrecursionlimit(10**7)

n = int(input())
graph = [[] for _ in range(n+1)]

# 가장 먼 곳을 찾는 dfs함수
def dfs(x, w):
    for i in graph[x]:
        a, b = i
        if distance[a] == -1:
            distance[a] = w+b
            dfs(a, w+b)

for _ in range(n-1):
    a, b, c = map(int, input().split())
    graph[a].append((b, c))
    graph[b].append((a, c))

distance = [-1]*(n+1)
distance[1] = 0
dfs(1, 0)

start = distance.index(max(distance))
distance = [-1]*(n+1)
distance[start] = 0
dfs(start, 0)

print(max(distance))
```

#### 개선할 점 & 얻은 점
트리의 지름을 찾는 방법에 대해서 배워갈 수 있었다. 증명이 솔직히 이해가 잘 안 되지만 좋은 풀이가 정말 많은 것 같다.