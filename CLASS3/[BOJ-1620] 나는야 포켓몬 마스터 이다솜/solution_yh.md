## BOJ 1620 나는야 포켓몬 마스터 이다솜
#### 문제 접근 전략
입력 개수, 문제 유형을 보니 key, value 쌍을 이용하는 문제로 보임.  
list나 배열 자료형을 이용할 수도 있지만  
.index() 메소드를 이용할 때 100,000*100,000의 시간복잡도가 소요될 수 있어 보임.  
dictionary 객체를 활용하는 것이 효율적인 것으로 보임.

##### 첫번째 풀이 - 정답
포켓몬이 등록된 번호와 이름을 둘다 key, value 쌍으로 만들어 주어  
번호 -> 이름, 이름 -> 번호 두 조건이 만족되도록 풀이함.
```python
import sys
input = sys.stdin.readline

n, m = map(int, input().split())
arr = dict()
for i in range(n):
    s = input().rstrip()
    arr[s], arr[str(i+1)] = str(i+1), s

for _ in range(m):
    print(arr[input().rstrip()])
```

##### 두번째 풀이 - 시간초과
당연한 결과이다.  
인덱싱하는 과정에서 O(N)만큼이 M번 소요될 수 있기에 시간초과가 났다.
```python
import sys
input = sys.stdin.readline

n, m = map(int, input().split())
arr = list()
for i in range(n):
    arr.append(input().rstrip())

for _ in range(m):
    s = input().rstrip()
    if s.isdigit():
        print(arr[int(s)-1])
    else:
        print(arr.index(s)+1)
```

#### 개선할 점 & 얻은 점
key, value 쌍을 이용한 단순한 문제이다.  
list 자료형과의 시간복잡도를 고려할 수 있는 좋은 문제로, list 객체를 이용하여  
구현할 수 있는지도 찾아보면 좋을 것 같다.