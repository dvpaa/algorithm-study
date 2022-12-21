## 문제

https://www.acmicpc.net/problem/11724


## 풀이

DFS 또는 BFS로도 풀 수 있지만 서로소 집합을 이용해서 풀어보았다.

각 연결요소를 하나의 집합으로 묶었고 부모 노드의 번호가 같으면 하나의 연결요소로 판단했다.


### 코드

```python
import sys
input = sys.stdin.readline


def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)

    if a < b:
        parent[b] = a
    else:
        parent[a] = b


def find_parent(parent, x):
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x])
    return parent[x]


N, M = map(int, input().split())
parent = [x for x in range(N+1)]
for _ in range(M):
    u, v = map(int, input().split())
    union_parent(parent, u, v)

result = set()
for i in range(1, N+1):
    result.add(find_parent(parent, i))

print(len(result))
```
