## BOJ 1780 종이의 개수
#### 문제 접근 전략
만일 이중 for문을 돌고 숫자가 다른 것이 있다면 크기를 3으로 나눈 후,  
9개의 사각형을 다시 재귀함수로 호출하는 방식으로 풀면 될 것 같음.
##### 첫번째 풀이 - 정답
예전에 풀이에서 -1, 0, 1의 개수이기 때문에  
result에는 +1의 인덱스를 해주면 간단히 값을 추가할 수 있었던 것이 떠올라 똑같이 해주었음.  
구현부분에서 조금 헷갈린게 있어서 시간이 조금 소요되었지만  
무리없이 풀 수 있는 문제였음.
```python
import sys

N = int(input())
arr = []
for _ in range(N):
    arr.append(list(map(int, sys.stdin.readline().split())))
result = [0]*3

def check(x, y, n):
    first = arr[x][y]
    for i in range(x, x+n):
        for j in range(y, y+n):
            if arr[i][j] != first:
                return False
    return True

def run(x, y, n):
    if not check(x, y, n):
        for i in range(x, x+n, n//3):
            for j in range(y, y+n, n//3):
                run(i, j, n//3)
    else:
        result[arr[x][y]+1] += 1

run(0, 0, N)
for i in result:
    print(i)
```
##### 두번째 풀이 - 5달 전
전체적인 로직은 똑같은 것을 알 수 있음.  
solve함수에서 이중for문을 도는 과정을 +*n으로 사용한 것이 인상적이지만,  
직관적인 이해로는 지금의 풀이가 더 낫다고 생각함.  
isValid함수에서 첫번째 값을 비교 해줄 때 xy를 이용하여 구현한 것이 불필요한 코드사용을 없애는데 좋을 것 같음.  
(첫번째 풀이 first변수)
```python
import sys
input = sys.stdin.readline

def isValid(x, y, n):
    for i in range(x, x+n):
        for j in range(y, y+n):
            if graph[x][y] != graph[i][j]:
                return False
    return True

def solve(x, y, z):
    if isValid(x, y, z):
        result[graph[x][y] + 1] += 1
        return

    n = z//3
    for i in range(3):
        for j in range(3):
            solve(x+i*n, y+j*n, n)

n = int(input())
graph = [list(map(int, input().split())) for _ in range(n)]
result = [0]*3
solve(0, 0, n)
for i in range(3):
    print(result[i])
```

#### 개선할 점 & 얻은 점
오랜만에 풀어보는 재귀함수였지만 생각보다 논리적으로 풀 수 있어서 좋았음.  
예전에 사용했던 여러 테크닉들을 조금씩 상기시키면 좋을 것 같음.