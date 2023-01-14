## BOJ 1697 숨바꼭질
#### 문제 접근 전략
좌표가 최신화 될 때 마다 덱에 넣어준 후 비교 후 초기화 시켜주는 방식으로 풀이를 하면 될 것 같다.

##### 첫번째 풀이 - 정답
범위를 벗어나지 않게 해주었고 0 값일 때는 무조건 넣어주어야 하므로 분기 조건에 추가하였다.
```python
from collections import deque

n, k = map(int, input().split())
arr = [0]*100001
q = deque([n])
while True:
    x = q.popleft()
    if x == k:
        print(arr[k])
        break
    for i in [x-1, x+1, 2*x]:
        if 0<=i<=100000:
            if arr[i] <= arr[x]+1 and arr[i] != 0:
                continue
            q.append(i)
            arr[i] = arr[x]+1
```

##### 두번째 풀이 - 5달 전
간과한 것이 있었다. 이미 최소가 되어서 덱에 넣어주면 그 다음에 넣어지는 것들은  
자동으로 최소시간이 된다. 그러므로 분기조건을 없애줄 수 있다.
```python
from collections import deque

n, k = map(int, input().split())
graph = [-1] * 100001
graph[n] = 0
def bfs():
    q = deque([n])
    while q:
        x = q.popleft()
        if x == k:
            return graph[x]
        for nx in [x-1, x+1, 2*x]:
            if 0 <= nx <= 100000 and graph[nx] == -1:
                graph[nx] = graph[x] + 1
                q.append(nx)
print(bfs())
```

##### 세번째 풀이 - 정답
두번째 풀이를 참고하여 다시 풀어보았다.
```python
from collections import deque

n, k = map(int, input().split())
arr = [-1]*(100001)
arr[n] = 0
q = deque([n])
while True:
    x = q.popleft()
    if x == k:
        print(arr[k])
        break
    for i in [x-1, x+1, 2*x]:
        if 0<=i<=100000 and arr[i]==-1:
            q.append(i)
            arr[i] = arr[x]+1
```

#### 개선할 점 & 얻은 점
bfs문제를 되새김할 수 있는 문제였다.  
빠른 문제풀이를 위해 변수명 통일, 여러 테크닉을 다시 상기해야 할 것 같다.