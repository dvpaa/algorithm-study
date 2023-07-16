## BOJ 9375 패션왕 신해빈

#### 문제 접근 전략
옷을 입는 조합을 구하는 문제이다. 각 종류 별로 곱해주고 안 입는 경우를 고려해서 풀이해준다.
##### 첫번째 풀이 - 정답
```python
import sys
input = sys.stdin.readline

for _ in range(int(input())):
    n = int(input())
    wearlist = dict()
    for _ in range(n):
        name, wear = input().split()
        if wear in wearlist:
            wearlist[wear] += 1
        else:
            wearlist[wear] = 1
    count = 1
    for i in wearlist.keys():
        count *= wearlist[i] + 1
    print(count-1)
```
##### 개선할 점 & 얻은 점
카운터객체를 이용해서 풀이하면 더 간단하게 로직을 짤 수 있다. 