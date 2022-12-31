## BOJ 1764 듣보잡
#### 문제 접근 전략
겹치는지 안겹치는지 set객체를 사용하면 편리할 것으로 보임.  
문제 풀이를 두가지로 나누어 볼 것이다.  

첫번째는 입력을 한 번에 받으면서 set객체에 input값이 존재한다면 list객체에 append,  
존재하지 않는다면, set객체에 add.  
두번째는 입력을 n, m 번 각각 받으면서 두 set객체를 만들고 교집합을 구하는 방법.

##### 첫번째 풀이 - 정답
set자료형의 in 연산 시 시간복잡도에 관해 지식이 부족하여  
key, value 형식의 dictionary를 이용하여 O(1)의 시간복잡도로 접근해주었다.
```python
import sys

n, m = map(int, input().split())
arr1 = dict()
arr2 = list()
for i in range(n+m):
    s = sys.stdin.readline().rstrip()
    if arr1.get(s):
        arr2.append(s)
    else:
        arr1[s] = 1
arr2.sort()
print(len(arr2))
for i in arr2:
    print(i)
```

##### 두번째 풀이 - 정답
set객체에 in 연산자를 해본 결과로 위 풀이보다 약 30ms정도 빨라졌다.(BOJ 기준)
```python
import sys

n, m = map(int, input().split())
arr1 = set()
arr2 = list()
for i in range(n+m):
    s = sys.stdin.readline().rstrip()
    if s in arr1:
        arr2.append(s)
    else:
        arr1.add(s)
arr2.sort()
print(len(arr2))
for i in arr2:
    print(i)
```

##### 세번째 풀이 - 정답
두 set객체를 만든 후 교집합을 해준 결과, 두번째 풀이보다 20ms 정도 빨라졌다.
```python
import sys

n, m = map(int, input().split())
arr1 = set()
arr2 = set()
for i in range(n):
    arr1.add(sys.stdin.readline().rstrip())

for j in range(m):
    arr2.add(sys.stdin.readline().rstrip())
    
result = sorted(list(arr1 & arr2))
# result = sorted(list(arr1.intersection(arr2)))
print(len(result))
for i in result:
    print(i)
```

#### 개선할 점 & 얻은 점
set자료형에 in 연산자 수행 시 시간복잡도가 O(1)임을 파악했다.  
set자료형도 해시함수와 해시테이블을 이용하는 자료구조이기 때문에 요소 접근에 O(1)의 시간복잡도가 발생한다.  
두번째 풀이와 세번째풀이의 차이점은 조건문에서 발생하는 시간복잡도인 것 같아 보인다.  
set자료형의 union연산의 시간복잡도는 O(n+m), intersection연산의 시간복잡도는 O(n or m)으로 둘 중에 더 많은 요소를 가진 객체의 크기만큼 소요된다.  
이 set자료형의 연산들의 시간복잡도를 잘 고려하여 문제풀이에 적용해야할 것 같다.