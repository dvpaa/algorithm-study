## BOJ 11725 트리의 부모 찾기

#### 문제 접근 전략
비순회 트리 문제이기 때문에 단순히 dfs를 통해서 말단 노드까지 내려가며 부모노드를 설정해주면 된다.
##### 첫번째 풀이 - 정답
클래스를 이용하여 실제 트리처럼 구현해보았다.  
노드의 개수가 많아서 재귀스택제한을 높여주었다.
```python
import sys
input = sys.stdin.readline
sys.setrecursionlimit(int(1e6))

class Node:
    def __init__(self, num):
        self.num = num
        self.edges = set()

    def get_num(self):
        return self.num

    def set_edge(self, other):
        self.edges.add(other)

    def get_edges(self):
        return self.edges

class Tree:
    def __init__(self, n):
        self.nodes = [Node(i) for i in range(n+1)]
        self.parents = [0]+[1]+[0]*(n-1)

    def add_node(self, node:int, other:int):
        self.nodes[node].set_edge(other)
        self.nodes[other].set_edge(node)

    def set_parent(self, root):
        for edge in root.get_edges(): # 여기부터 다시 AttributeError: 'Node' object has no attribute 'get_edges'
            if not self.parents[edge]: # 부모가 정해지지 않은 경우
                self.parents[edge] = root.get_num()
                self.set_parent(self.nodes[edge])

    def print_parents(self):
        for p in self.parents[2:]:
            print(p)

    def get_root(self):
        return self.nodes[1]

n = int(input())
tree = Tree(n)
for _ in range(n-1):
    a, b = map(int, input().split())
    if a != b:
        tree.add_node(a, b)
tree.set_parent(tree.get_root())
tree.print_parents()
```

##### 두번째 풀이 - 정답
단순한 dfs풀이이다. 위 로직과 다른게 없지만 클래스를 이용하지 않고 훨씬 단순하게 푼 코드이다.
```python
import sys
input = sys.stdin.readline
sys.setrecursionlimit(int(1e6))

n = int(input())
graph = [[] for _ in range(n+1)]
visited=[False]*(n+1)
parents=[0]*(n+1)
def dfs(root):
    for i in graph[root]:
        if not visited[i]:
            parents[i] = root
            visited[i] = True
            dfs(i)

for _ in range(n-1):
    a, b = map(int, input().split())
    if a != b:
        graph[a].append(b)
        graph[b].append(a)

dfs(1)
for i in parents[2:]:
    print(i)
```
#### 개선할 점 & 얻은 점
오랜만에 트리 자료구조를 구현해보았다. 물론 트리에 더 다양한 조건과 속성들이 있겠지만 상기시키는데 좋은 문제였다. 