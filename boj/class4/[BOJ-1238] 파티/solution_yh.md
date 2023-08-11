## BOJ 1238 파티

#### 문제 접근 전략
전형적인 다익스트라 문제로 보인다 거리를 초기화 하기 위한 조금의 테크닉을 추가하면 될 것 같다.

##### 첫번째 풀이 - 정답
n번째 노드에서 x로가는 거리는 각 다익스트라 결과 마다 더해주고,  
x에서 n번째 노드로 가는 최단 거리 테이블은 모두 더해주면 왕복 최소 거리가 된다.
```python
import heapq
import sys
input = sys.stdin.readline
INF = int(1e9)

n, m, x = map(int, input().split())
graph = [[] for _ in range(n+1)]
for _ in range(m):
    s, e, cost = map(int, input().split())
    graph[s].append((e, cost))

def dijkstra(start):
    distance = [INF]*(n+1)
    distance[start] = 0

    q = []
    heapq.heappush(q, (0, start))
    while q:
        dist, now = heapq.heappop(q)
        if distance[now] < dist:
            continue
        for i in graph[now]:
            cost = dist + i[1]
            if cost < distance[i[0]]:
                distance[i[0]] = cost
                heapq.heappush(q, (cost, i[0]))

    return distance

result = [0]*(n+1)
for i in range(1, n+1):
    tmp = dijkstra(i)
    if i == x:
        for j in range(1, n+1):
            result[j] += tmp[j] # x -> n으로 향하는 최단 거리를 모두 더해준다.
    else:
        result[i] += tmp[x] # 각 n -> x로 향하는 최단거리를 결과 테이블에 더한다

print(max(result))
```

#### 개선할 점 & 얻은 점
전형적인 다익스트라 문제로, 쉽게 풀 수 있었다. 최적화하는 부분만 조금 더 신경쓰면 좋을 것 같다.