## 문제
https://www.acmicpc.net/problem/1620

## 풀이
### 설명
딕셔너리 두 개를 사용해서 풀었다.

input이 최대 100,000개여서 치환하여 사용하였다.


## 코드
```python
input = stdin.readline

N, M = map(int, input().split())
number_key = {}
name_key = {}

for i in range(1, N+1):
    po_name = input().rstrip()
    name_key[po_name] = i
    number_key[i] = po_name

for _ in range(M):
    key = input().rstrip()
    if key in name_key:
        print(name_key[key])
    else:
        print(number_key[int(key)])
```
