## BOJ 2798 블랙잭

#### *문제 접근 전략
고르는 카드의 수가 3장으로 fix되어있고 고른 카드의 합이 m을 넘지 않으면 되기에  
모든 경우의 수를 반복문으로 따져보거나 조합을 이용하여 풀이함.  
조합으로 푸는 방법이 효율적인 것 같음.


##### 첫번째 풀이 - 정답
조합을 이용하여 풀이를 시도하였다.  
굳이 완전탐색하지 않고 3개의 수를 뽑는 경우의 수 중에서만 골라서  
시간복잡도 효율을 증가시킬 수 있게 하였다.
```python
from itertools import combinations
n, m = map(int, input().split())
arr = list(map(int, input().split()))
result = 0
for i in combinations(arr, r=3):
    tmp = sum(i)
    if result < tmp <= m:
        result = tmp
print(result)
```

##### 두번째 풀이 - 정답
완전탐색 방법으로 풀어본 코드이다.  
조합 풀이에 비해서 조건이 많고 기본적으로 O(100^3)이 소요되니 시간복잡도면에서도 비효율적이었다.
```python
n, m = map(int, input().split())
arr = list(map(int, input().split()))

result = 0
for i in range(n):
    for j in range(n):
        for k in range(n):
            if i != j and j != k and i != k:
                tmp = arr[i] + arr[j] + arr[k]
                if result < tmp <= m:
                    result = tmp
print(result)                    
```

#### 개선할 점 & 얻은 점
뽑는 경우의 수가 3장으로 제한되어 있었기 때문에 문제의 난이도가 낮은 것으로 보인다.  
차후 문제에서 개수는 최대로 하면서 M에 최대한 가까운 카드들과 그들의 합을 출력하는 문제로도 이용될 수 있을 것 같다.  
itertools라이브러리 상 시간복잡도가 r값에 따라 매우 높아지니 조합을 사용하는 풀이는 힘들 것 같다.