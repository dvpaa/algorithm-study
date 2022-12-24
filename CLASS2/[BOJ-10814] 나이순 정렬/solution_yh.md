BOJ 10814 나이순 정렬

#### *문제 접근 전략
조건에 따라 정렬하면 되는 문제. 나이순 정렬 후 먼저 가입한 순서로 정렬하는  
sort기법 사용

##### 첫번째 풀이 - 정답
나이순 정렬은 어려울게 없고 우선순위 정렬하는 것에 있어서  
반복문 실행에 따라 각 정보 뒤에 번호를 매겨주는 알고리즘을 짰다.  
문제없이 동작하였다.
```python
import sys

n = int(input())
arr = []
for i in range(n):
    tmp = sys.stdin.readline.split()
    tmp.append(i)
    arr.append(tmp)
arr.sort(key=lambda x:(int(x[0]), x[2]))
for i in range(n):
    print(arr[i][0], arr[i][1])
```

##### 두번째 풀이 - 피드백
key로 x[0] 첫번째 인자에 대해 정렬 시 어짜피 원소는 들어온 순서대로  
정렬되어있기 때문에 굳이 번호를 매겨줄 필요가 없음.
```python
import sys

n = int(input())
arr = []
for i in range(n):
    arr.append(sys.stdin.readline().split())
arr.sort(key=lambda x:(int(x[0])))
for i in range(n):
    print(*arr[i])
```

#### 개선할점 & 얻은 점
빠르게 넘어가겠다.