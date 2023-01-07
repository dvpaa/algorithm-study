## 문제

https://www.acmicpc.net/problem/9019


## 풀이

### 설명

명령어의 조합으로 target number을 만드는 문제이다. 명령어는 4개(D,S,L,R), BFS로 접근하였다.

명령어에 따라 결과값을 리턴하는 함수를 작성해주었고 큐에 조합들을 하나 씩 넣고 지나온 경로를 늘려주었다.

로직에는 문제가 없는 것 같은데 계속해서 시간 초과 판정을 받았다.

### 처음 작성한 코드
```python
from collections import deque


def convert_string(operator: str, val: int) -> int:
    if operator == "D":
        return 2 * val % 10000

    elif operator == "S":
        return 9999 if val == 0 else val-1

    elif operator == "L":
        str_num = "0" * (4 - len(str(val))) + str(val)
        return int(str_num[1] + str_num[2] + str_num[3] + str_num[0])

    elif operator == "R":
        str_num = "0" * (4 - len(str(val))) + str(val)
        return int(str_num[3] + str_num[0] + str_num[1] + str_num[2])


std_op = ["D", "S", "L", "R"]
for _ in range(int(input())):
    init_val, target_val = map(int, input().split())
    mem = dict()
    for op in std_op:
        mem[op] = convert_string(op, init_val)

    queue = deque(["D", "S", "L", "R"])
    while True:
        operator = queue.popleft()
        if mem[operator] == target_val:
            print(operator)
            break
        else:
            for op in std_op:
                new_op = operator + op
                mem[new_op] = convert_string(op, mem[operator])
                queue.append(new_op)
```


### 시간을 단축시킨 방법
1. 우선 visited 리스트를 만들어서 이미 방문한 노드는 배제시켰다.(예를 들어 LR 명령어같은 경우)
2. 지나온 경로를 계속해서 문자열로 업데이트 시키지않고 자신이 어디서 어떤 명령어로 왔는지만 기억해두었다.
    - 파이썬의 경우 문자열을 `+` 연산으로 업데이트하면 새로운 문자열을 만들어 반환하기 때문에 O(N)이다.
    - 마지막에 자신이 온 노드로 계속해서 찾아가면서 명령어를 조합했다.
3. pypy3로 제출
    - 도저히 python3로는 어떻게 통과해야할지 모르겠다...

### 개선한 코드
```python
from collections import deque
import sys

input = sys.stdin.readline


def convert_string(operator: str, val: int) -> int:
    if operator == "D":
        return 2 * val % 10000

    elif operator == "S":
        return 9999 if val == 0 else val-1

    elif operator == "L":
        str_num = "0" * (4 - len(str(val))) + str(val)
        return int(str_num[1] + str_num[2] + str_num[3] + str_num[0])

    elif operator == "R":
        str_num = "0" * (4 - len(str(val))) + str(val)
        return int(str_num[3] + str_num[0] + str_num[1] + str_num[2])


def bfs(init_val: int) -> None:
    queue = deque([init_val])
    while True:
        current_val = queue.popleft()
        for op in std_op:
            new_val = convert_string(op, current_val)
            if not visited[new_val]:
                visited[new_val] = True
                prev[new_val] = (op, current_val)
                if new_val == target_val:
                    return
                queue.append(new_val)


std_op = ["D", "S", "L", "R"]

for _ in range(int(input())):
    init_val, target_val = map(int, input().split())
    visited = [False] * 10000
    prev = [None] * 10000

    bfs(init_val)

    result = []
    while True:
        if prev[target_val] is None or target_val == init_val:
            print("".join(result[::-1]))
            break

        result.append(prev[target_val][0])
        target_val = prev[target_val][1]
```

9676ms가 나왔다...

추가적으로 `convert_string`함수에서 L과 R명령어도 문자열연산이 아닌 수학적인 연산으로 O(1)로 접근해서 개선시켜보았다.

```python
def convert_string(operator: str, val: int) -> int:
    if operator == "D":
        return 2 * val % 10000

    elif operator == "S":
        return 9999 if val == 0 else val-1

    elif operator == "L":
        return 10*(val % 1000) + val // 1000

    elif operator == "R":
        return (val // 10) + 1000 * (val % 10)
```

6660ms로 조금 더 단축시킬 수 있었다.
