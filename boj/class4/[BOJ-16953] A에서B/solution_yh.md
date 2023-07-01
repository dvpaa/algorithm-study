## BOJ 16953 A->B

#### 문제 접근 전략
연산 크기가 1로 정해진 bfs문제이다. top-down 방식의 풀이도 있지만 간단하게 보텀업으로 풀이해보았다.

##### 첫번째 풀이 - 정답
연산 중복방지를 위해 사전형 하나를 추가해주었다.
```python
from collections import deque

a, b = map(int, input().split())
d = dict()
def bfs(start):
    q = deque()
    q.append((start, 0))
    while q:
        x, count = q.popleft()
        if x == b:
            return count+1
        for i in [x*2, x*10+1]:
            if i <= b:
                if i not in d:
                    q.append((i, count+1))
                    d[i] = 1
    return -1
print(bfs(a))
```

#### 개선할 점 & 얻은 점
전형적인 bfs문제이지만 문제 해석 시에 bfs문제로 풀 수 있다는 것을 깨닫기가 어려웠다. bfs로 최단거리 또는 최단 연산 수행 가능하다는 것을 항상 숙지하자. 