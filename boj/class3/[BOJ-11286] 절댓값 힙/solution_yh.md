## BOJ 11286 절댓값 힙

#### 문제 접근 전략
파이선 모듈 heapq를 사용하여 

##### 첫번째 풀이 - 정답
최소/최대힙 2개를 만들어 풀이하였다. 최소힙에는 양수를 넣고 최대힙에는 음수를 넣어 둘 다 존재할 시 루트노드의 값을 비교하여 절댓값을 비교해주었다.
```python
from heapq import heappush, heappop
import sys
input = sys.stdin.readline

pos_q = []
neg_q = []
for _ in range(int(input())):
    x = int(input())
    if x:
        if x > 0:
            heappush(pos_q, x)
        else:
            heappush(neg_q, -x)
    else:
        if pos_q and neg_q:
            if pos_q[0] >= neg_q[0]:
                print(-heappop(neg_q))
            else:
                print(heappop(pos_q))
        elif pos_q:
            print(heappop(pos_q))
        elif neg_q:
            print(-heappop(neg_q))
        else:
            print(0)
```

##### 두번째 풀이 - 풀이 참고
최소힙에 절댓값을 기준으로 삽입하고 만일 값이 같다면 투플의 두번째 요소를 비교하여 정렬해주는 테크닉을 이용한 방식이다.  
더욱 간단하게 코드를 짤 수 있다. 그러나 하나의 q를 우선순위로 정렬하기 때문에 내부적으로는 조금 더 오래 걸린다.
```python
from heapq import heappush, heappop
import sys
input = sys.stdin.readline

q = []
for _ in range(int(input())):
    x = int(input())
    if x:
        heappush(q, (abs(x), x))
    else:
        if q:
            print(heappop(q)[1])
        else:
            print(0)
```

#### 개선할 점 & 얻은 점
음수를 저장할 때 테크닉을 똑같은 방식으로 절댓값으로 저장하면 된다는 것을 알 수 있었던 문제이다.