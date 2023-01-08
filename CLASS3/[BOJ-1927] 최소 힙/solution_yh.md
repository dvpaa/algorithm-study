## BOJ 1927 최소 힙
#### 문제 접근 전략
최소 힙 구현 문제이다.  
최소 값을 출력하는 문제이기 때문에 그냥 heappop을 이용하면 될 것이다.
##### 첫번째 풀이 - 정답
```python
import heapq
import sys

h = []
for _ in range(int(input())):
    num = int(sys.stdin.readline().rstrip())
    if num == 0:
        if h:
            print(heapq.heappop(h))
        else:
            print(0)
    else:
        heapq.heappush(h, num)
```
##### 두번째 풀이 - 8달 전
자료구조를 배울 때 시점이다.  
쓸데없는 리스트 객체와 객체의 크기를 구하는 연산을 사용하였다.
```python
import heapq
import sys
n = int(input())
k = []
h = []
for i in range(n):
    k.append(sys.stdin.readline())
    if int(k[i]) == 0:
        if len(h) == 0:
            print(0)
        else:
            print(heapq.heappop(h))
    else:
        heapq.heappush(h, int(k[i]))

```
##### 개선할 점 & 얻은 점
최소 힙 문제를 푸는데 가장 기초적인 문제로 생각한다.  
최대 힙 구현이 나오면 '-'를 해주는 테크닉도 생각이 났다.  
다음 힙 관련 문제가 나올 때를 대비하자.