## BOJ 11723 집합
#### 문제 접근 전략
집합자료형 구현 문제이다.  
연산 조건에 따라 쉽게 코드를 정의하면 될 것 같다.  
다만 input 개수와 시간, 메모리 제한이 있기 때문에 고려할 요소가 있어보인다.  
##### 첫번째 풀이 - 정답
remove 연산은 메소드 실행 시 해당 원소가 집합에 원소가 아니라면 
Error를 일으킨다.  
아무일도 일어나지 않기 위해 discard 메소드를 사용하였다.  

check, toggle 연산 시에는 해당 원소가 집합 내에 존재하는지 체크해야하므로 부분집합 연산을 이용하여 체크해주었다.

all 연산 시에 매 수행마다 range(1,21)을 연산하므로
최대 300만 x 20 + a로 시간초과가 날 수도 있겠다 생각하여
그러한 집합을 만들어 놓고 copy하는 방식을 하였다.  
메모리도 4MB 제한이어서 중간에 del 시켜주었다.
```python
import sys

s = set()
s1 = set(range(1, 21))
for i in range(int(input())):
    l = sys.stdin.readline().split()
    command, num = l[0], l[-1]
    if command == 'add':
        s.add(int(num))
    elif command == 'remove':
        s.discard(int(num))
    elif command == 'check':
        print(1) if {int(num)}.issubset(s) else print(0)
    elif command == 'toggle':
        if {int(num)}.issubset(s):
            s.remove(int(num))
        else:
            s.add(int(num))
    elif command == 'all':
        del s
        s = s1.copy()
    else:
        s.clear()
```
##### 두번째 풀이 - 정답
시간초과가 나는지 확인해보기 위하여, 
매 all 연산 시에 새로운 set을 정의해보았다.  
시간이 48ms만큼 느려지긴했지만 통과되었다.  
내가 생각한 만큼 시간이 걸리지 않거나, 파이썬이 빠르거나,  
test case에 모두 all연산인 경우가 없는 것 같다.  
```python
import sys

s = set()
for i in range(int(input())):
    l = sys.stdin.readline().split()
    command, num = l[0], l[-1]
    if command == 'add':
        s.add(int(num))
    elif command == 'remove':
        s.discard(int(num))
    elif command == 'check':
        print(1) if {int(num)}.issubset(s) else print(0)
    elif command == 'toggle':
        if {int(num)}.issubset(s):
            s.remove(int(num))
        else:
            s.add(int(num))
    elif command == 'all':
        del s
        s = set(range(1, 21))
    else:
        s.clear()
```

##### 세번째 풀이 - 코드 참고
set이 iterable 객체인 것을 확인한 후 in 연산을 사용하여 풀이하였다.  
약 300ms가 단축되었다.
```python
import sys

s = set()
s1 = set(range(1, 21))
for i in range(int(input())):
    command = sys.stdin.readline().split()
    if command[0] == 'add':
        s.add(int(command[1]))
    elif command[0] == 'remove':
        s.discard(int(command[1]))
    elif command[0] == 'check':
        print(1) if int(command[1]) in s else print(0)
    elif command[0] == 'toggle':
        if int(command[1]) in s:
            s.remove(int(command[1]))
        else:
            s.add(int(command[1]))
    elif command[0] == 'all':
        del s
        s = s1.copy()
    else:
        s.clear()
```

#### 개선할 점 & 얻은 점
set 자료형의 메소드를 자주 애용하지는 않기에 vscode ui에 뜨는 메소드 설명을 읽어보았다.  
차후 set 자료형 구현 시에 익숙해질 필요가 있다고 느꼈고, 아주 유용한 자료형이기에 set으로 다양한 접근을 해보면 좋을 것 같다.