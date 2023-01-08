## BOJ 11279 최대 힙
#### 문제 접근 전략
최대 힙 구현 문제이다.  
최대 값을 출력하는 문제이기 때문에 heappush 시에 '-'를 붙여 절댓값 내림차순으로 바꾸어 준 뒤,  
heappop 시 다시 -1을 곱하여 원래의 값을 출력하여 준다.
##### 첫번째 풀이 - 정답
```python
import heapq
import sys

h = []
for _ in range(int(input())):
    num = int(sys.stdin.readline().rstrip())
    if num == 0:
        if h:
            print(-heapq.heappop(h))
        else:
            print(0)
    else:
        heapq.heappush(h, -num)
```
##### 두번째 풀이 - 8달 전
```python
import sys
import heapq
n = int(input())
k = []
h = []
for i in range(n):
    k.append(sys.stdin.readline())
    if int(k[i]) == 0:
        if len(h) == 0:
            print(0)
        else:
            print(heapq.heappop(h)[1])
    else:
        heapq.heappush(h, (-int(k[i]), int(k[i])))
```
##### 개선할 점 & 얻은 점
힙 연산 시 필요한 테크닉 두 가지를 배웠다.  
heap은 다익스트라 알고리즘에서도 사용되는 자료구조로 준비를 잘해야 할 필요가 있다.