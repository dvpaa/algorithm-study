## 문제

https://www.acmicpc.net/problem/11723

## 풀이

단순히 파이썬의 집합 자료형을 이용하여 풀 수 있었다. 다만, 시간 복잡도를 잘 생각해서 풀었는데 계속 시간초과가 났다.

생각해보니 input의 개수가 300만개여서 영향을 줬다. 문제의 시간 복잡도에만 초점을 두었던 것 같다.

### 코드

```python
import sys

input = sys.stdin.readline

S = set()

for _ in range(int(input())):
    operation = input().rstrip().split(" ")

    if operation[0] == "add":
        S.add(int(operation[1]))
        
    elif operation[0] == "remove":
        if int(operation[1]) in S:
            S.remove(int(operation[1]))
            
    elif operation[0] == "check":
        print(1) if int(operation[1]) in S else print(0)
        
    elif operation[0] == "toggle":
        if int(operation[1]) in S:
            S.remove(int(operation[1]))
        else:
            S.add(int(operation[1]))
            
    elif operation[0] == "all":
        S = {x for x in range(1, 21)}
        
    elif operation[0] == "empty":
        S = set()

```
