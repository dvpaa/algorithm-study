## BOJ 1931 회의실 배정
#### 문제 접근 전략
회의의 개수를 최대로 하기위해선 회의 시간이 짧을 수록 좋으며 끝시간이 같다면 가장 베스트.  
정렬알고리즘을 이용하여 끝시간으로 정렬 후 시작시간으로 정렬을 하면 자동으로 가능한 시간의 경우가 가장 많아지고 그 상태에서 시작시간이 이전 끝시간 보다 크거나 같은 경우에만 회의로 사용하면 된다.  
##### 첫번째 풀이 - 오답
끝시간을 먼저 정렬해야 한다는 것을 깨닫지 못했다.  
조건문을 사용하여 88프로까지 정답이 되었지만, 테스트케이스에서 걸렸다.  
끝시간이 작지만 시작시간이 같은 경우에 대해서 처리하지 못하였다.  
조건문을 여러개 달면 풀 수 있겠지만 더 나은 풀이가 있을 것이라고 생각했고,  
계속해서 명료한 코드를 작성하려고 하다보니 시간만 오래걸렸다.
```python
import sys

n=int(input())
arr=[]
for _ in range(n):
    arr.append(list(map(int, sys.stdin.readline().rstrip().split())))
arr.sort(key=lambda x: (x[0], x[1]))

tmp=arr[0]
cnt=1
for s, e in arr[1:]:
    if e <= tmp[1]:
        tmp = [s, e]
    elif s >= tmp[1]:
        tmp = [s, e]
        cnt += 1
print(cnt)
```

##### 두번째 풀이 - 정답
6달 전 풀이를 참고한 코드이다.  
끝 시간을 기준으로 정렬만 해주면 쉽게 풀리는 문제였다.
```python
import sys

n=int(input())
arr=[]
for _ in range(n):
    arr.append(list(map(int, sys.stdin.readline().split())))
arr.sort(key=lambda x:(x[1], x[0]))

cnt, end = 0, 0
for s, e in arr:
    if s >= end:
        end = e
        cnt += 1
print(cnt)
```

##### 세번째 풀이 - 6달 전
리스트객체로 만들어서 append시키는 것이 생각보다 많은 메모리를 차지하였다.  
또한 튜플 객체를 만들고 append시키는 것보다 두 수를 괄호로 묶고(tuple화) append시키는게  
시간복잡도에서 많은 차이가 났다. 잘 모르겠다.
```python
import sys
n = int(input())
array = []
for i in range(n):
    a, b = map(int, sys.stdin.readline().split())
    array.append((a, b))
array.sort(key=lambda x:(x[1], x[0]))

count, end = 0, 0
for s, e in array:
    if s >= end:
        count += 1
        end = e
print(count)
```

##### 개선할 점 & 얻은 점
그리디문제로서 핵심을 파악하지 못했던 문제이다.  
그리디문제 특성상 정렬과 함께 나오며 현재 시점에서 가장 좋은 선택을 하는 알고리즘으로  
너무 많은 조건을 생각했던 것 같다.