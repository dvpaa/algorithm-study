## 문제

https://www.acmicpc.net/problem/1764


## 풀이

집합 자료형으로 받아서 교집합을 구했다. 시간은 최대 2초로 충분하다고 판단하여 시간복잡도에대한 처리는 따로 진행하지 않았다.


### 코드

```python
N, M = map(int, input().split())
n_hear = {input() for _ in range(N)}
n_see = {input() for _ in range(M)}


inter = sorted(list(n_hear.intersection(n_see)))
print(len(inter))
print(*inter, sep='\n')
```
