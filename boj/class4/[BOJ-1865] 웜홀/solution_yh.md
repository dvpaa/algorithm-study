## BOJ 1865 웜홀

#### 문제 접근 전략
최단경로 알고리즘을 사용, 시작 위치로 거쳐오는 경우에 거리가 음의 크기라면 YES를 출력하면 될 것 같다.

##### 첫번째 풀이 - 32% 시간 초과
```python
import sys
from heapq import heappop, heappush

input = sys.stdin.readline
INF = int(1e9)

for _ in range(int(input())):
    n, m, w = map(int, input().split())
    graph = [[] for _ in range(n+1)]
    min_table = [[INF]*(n+1) for _ in range(n+1)] # i -> j로 가는 도로 사이의 최소 길이
    for _ in range(m):
        s, e, t = map(int, input().split())
        if min_table[s][e] > t: # 최소 크기의 도로만 사용하기 위해서(성능 향상)
            min_table[s][e] = t
            graph[s].append((e, t))
            graph[e].append((s, t))
    for _ in range(w):
        s, e, t = map(int, input().split())
        graph[s].append((e, -t))

    def dijkstra(start):
        q = []
        heappush(q, (0, start))
        distance = [INF] * (n+1)
        distance[start] = 0
        while q:
            dist, now = heappop(q)
            if now == start and dist < 0:
                return True
            if dist > distance[now]:
                continue
            for i in graph[now]:
                cost = dist + i[1]
                if distance[i[0]] > cost:
                    distance[i[0]] = cost
                    heappush(q, (cost, i[0]))
        return False
    def solve():
        for i in range(1, n+1):
            if dijkstra(i):
                return "YES"
        return "NO"
    print(solve())

```

##### 두번째 풀이 - 다른 사람 풀이 참고
벨만포드 풀이이다. 간선 수만큼 반복해주어 음의 사이클을 판별해주었다.
```python
import sys
input = sys.stdin.readline
INF = int(1e9)

for _ in range(int(input())):
    n, m, w = map(int, input().split())
    edges = []
    dist = [INF] * (n+1)

    for i in range(m+w):
        s, e, t = map(int, input().split()) # 노드, 인접 노드, 가중치
        if i >= m:
            t = -t
        else:
            edges.append((e, s, t))
        edges.append((s, e, t))

    def bf(): # O(VE)
        for i in range(n): # 정점 수만큼 반복 V
            for j in range(len(edges)): # 간선 수만큼 반복 E
                cur, next, cost = edges[j]
                if dist[next] > dist[cur] + cost:
                    dist[next] = dist[cur] + cost
                    if i == n-1: # n-1번 이후 반복에도 값이 갱신되면 음수 순환 존재
                        return "YES"
        return "NO"

    print(bf())
```

#### 개선할 점 & 얻은 점
다익스트라 알고리즘은 음의 가중치가 존재할 때는 사용할 수 없다.   
거리 초기화 시 계속해서 음의 가중치만큼 줄어들어 무한사이클이 발생하기 때문이다.  
음의 간선이 존재할 시에는 벨만포드 알고리즘을 활용하여 최단경로를 초기화 & 무한 사이클 판별이 가능하다.