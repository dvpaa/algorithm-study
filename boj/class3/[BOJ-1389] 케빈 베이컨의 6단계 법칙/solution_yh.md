## BOJ 1389 케빈 베이컨의 6단계 법칙

#### 문제 접근 전략
연결된 노드 간의 거리가 1인 최단거리 문제이다. 모든 노드에 대해서 다익스트라를 적용하여 최소 케빈 베이컨 수를 구하면 된다.

##### 첫번째 풀이 - 정답
```python
import sys
import heapq
input = sys.stdin.readline
INF = int(1e9)

n, m = map(int, input().split())
graph = [[] for _ in range(n+1)]
for _ in range(m):
    a, b = map(int, input().split())
    graph[a].append((1, b))
    graph[b].append((1, a))
def dijkstra(start):
    distance = [INF]*(n+1)
    q = []
    distance[start] = 0
    heapq.heappush(q, (0, start))

    while q:
        dist, now = heapq.heappop(q)
        if distance[now] < dist:
            continue

        for i in graph[now]:
            cost = dist + i[0]
            if cost < distance[i[1]]:
                distance[i[1]] = cost
                heapq.heappush(q, (cost, i[1]))

    return sum(distance[1:])

min_result = INF
min_index = 1
for i in range(1, n+1):
    result = dijkstra(i)
    if result < min_result:
        min_result = result
        min_index = i

print(min_index)
```
#### 개선할 점 & 얻은 점
힙 자료구조를 사용하지 않아도 되는 노드, 간선의 수지만 익숙해지기 위하여 힙 자료구조를 사용하였다. 