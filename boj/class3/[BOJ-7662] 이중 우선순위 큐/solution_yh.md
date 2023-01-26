## BOJ 7662 이중 우선순위 큐
#### 문제 접근 전략
최소 힙, 최대 힙을 구현하는 것은 어렵지 않은 문제이다.  
그러나 이것을 동기화 해주는 것이 가장 중요한 키포인트이다.  
1. 각 입력 시 마다의 고유 key값을 부여해준다.  
각각의 key값들은 반복문의 i번째로 할당된다.
2. 삭제 연산 시에는 해당 key값이 상대힙에서 삭제가 된 key값인지 확인해주며 pop을 해준다.  
3. 연산 후 쓰레기값이 존재할 수 있으므로 삭제 key값들을 한 번더 pop해준다.
##### 첫번째 풀이 - 시간초과
간단한 풀이로 구현해 보았다.  
remove과정에서 O(n)의 시간 때문에 당연히 시간초과가 날 것이라고 판단했고 당연히 시간초과가 발생했다.  
구현에 있어서는 가장 간단한 풀이라고 생각하지만 문제를 풀기에는 효율적이지 않은 코드이다.
```python
from heapq import heappush, heappop
import sys

for _ in range(int(input())):
    count = 0  # 숫자 개수
    q_min = [] # 최솟값을 출력하는 queue
    q_max = [] # 최댓값을 출력하는 queue

    for _ in range(int(input())):
        oper = sys.stdin.readline().split()
        if oper[0] == 'I':
            heappush(q_min, int(oper[1]))
            heappush(q_max, -int(oper[1]))
            count += 1
        else:
            if count:
                if oper[1] == '1': # 최댓값 삭제
                    q_min.remove(-heappop(q_max))
                else:
                    q_max.remove(-heappop(q_min))
                count -= 1

    if count:
        print(-heappop(q_max), heappop(q_min))
    else:
        print('EMPTY')
```
##### 두번째 풀이 - 정답 참고
입력 데이터가 최대 100만개이므로 고유 key값 리스트를 1000001 크기만큼 할당해주고 시작하였다.  
매 input 시에 해당 key값은 True로 바꿔 주어서 삭제되지 않은 값이라고 지정해주었다.  
반대로 삭제 연산 시 False를 해주었다.
```python
from heapq import heappush, heappop
import sys

for _ in range(int(input())):
    visited = [False] * 1_000_001
    q_min = []
    q_max = []

    for key in range(int(input())):
        oper = sys.stdin.readline().split()
        if oper[0] == 'I':
            heappush(q_min, (int(oper[1]), key))
            heappush(q_max, (-int(oper[1]), key))
            visited[key] = True

        elif oper[1] == '1':
            while q_max and not visited[q_max[0][1]]: 
                heappop(q_max)                        
            if q_max:
                visited[q_max[0][1]] = False
                heappop(q_max)

        else:
            while q_min and not visited[q_min[0][1]]:
                heappop(q_min)
            if q_min:
                visited[q_min[0][1]] = False
                heappop(q_min)
    
    while q_min and not visited[q_min[0][1]]:
        heappop(q_min)
    while q_max and not visited[q_max[0][1]]:
        heappop(q_max)
    
    print(-q_max[0][0], q_min[0][0]) if q_max and q_min else print('EMPTY')
```
#### 개선할 점 & 얻은 점
정말 어려운 문제였다.  
이중이라는 동기화 문제를 해결하기 위한 아이디어를 만들어 내는 것이 쉽지 않았다.  
확실히 tuple 자료구조가 문제의 난이도를 올리는데에 최적화 되어있다고 생각하였다.  
heap 자료구조를 이해하는데에도 많은 도움이 되었다.