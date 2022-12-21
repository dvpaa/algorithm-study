## 문제

https://www.acmicpc.net/problem/7662


## 풀이

### 처음 시도한 풀이

삽입 정렬을 사용해서 데이터를 입력할 때마다 매번 정렬을 수행하였다.

이미 정렬된 리스트이기 때문에 삽입 정렬의 효율성을 높여 $O(N)$으로 접근했고, 총 $O(N^2)$으로 풀었다.

time limit가 6초이긴 하지만 시간 초과 판정을 받았다.

### 코드
```python
import sys
input = sys.stdin.readline


def insertion_sort(arr):
    for end in range(1, len(arr)):
        to_insert = arr[end]
        i = end
        while i > 0 and arr[i - 1] > to_insert:
            arr[i] = arr[i - 1]
            i -= 1
        arr[i] = to_insert


for _ in range(int(input())):
    heap = []
    for __ in range(int(input())):
        oper = input().rstrip().split()

        if oper[0] == "I":
            heap.append(int(oper[1]))
            insertion_sort(heap)

        elif oper[0] == "D":
            if not heap:
                continue

            if oper[1] == "1":
                heap.pop(-1)
            elif oper[1] == "-1":
                heap.pop(0)

    if heap:
        print(heap[-1], heap[0])
    else:
        print("EMPTY")
```


### 맞은 풀이

max heap과 min heap을 각각 생성하여 pop할 때마다 동기화시키는 방식으로 접근했다

push할 때 공통 리스트를 참조하게하여 어느곳에서 pop하더라도 참조하는 리스트의 flag를 변경해줬다


### 코드

```python
import heapq
import sys

input = sys.stdin.readline

for _ in range(int(input())):
    min_heap = []
    max_heap = []
    for __ in range(int(input())):
        oper = input().rstrip().split()

        if oper[0] == "I":
            common_list = [int(oper[1]), True]
            heapq.heappush(min_heap, [int(oper[1]), common_list])
            heapq.heappush(max_heap, [-int(oper[1]), common_list])

        elif oper[0] == "D":
            if oper[1] == "1":
                while max_heap:
                    max_val = heapq.heappop(max_heap)
                    if max_val[1][1]:
                        max_val[1][1] = False
                        break

            elif oper[1] == "-1":
                while min_heap:
                    min_val = heapq.heappop(min_heap)
                    if min_val[1][1]:
                        min_val[1][1] = False
                        break

    flag = True
    while max_heap:
        val = heapq.heappop(max_heap)
        if val[1][1]:
            print(val[1][0], end=" ")
            flag = False
            break

    while min_heap:
        val = heapq.heappop(min_heap)
        if val[1][1]:
            print(val[1][0])
            break

    if flag:
        print("EMPTY")
```
