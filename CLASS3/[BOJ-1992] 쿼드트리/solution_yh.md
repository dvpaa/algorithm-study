## BOJ 1992 쿼드트리
#### 문제 접근 전략
전형적인 재귀문제로 보인다. 조건이 맞지 않을 시 4부분으로 분할시켜 준 후,  
분할이 되었을 때 괄호를 바로 출력해주는 방식으로 코드를 작성하면 될 것 같다. 
##### 첫번째 풀이 - 정답
백준 1780 종이의 개수 문제와 비슷한 형식이다.  
재귀는 스택으로 구현되므로 바로바로 출력시켜도 상관이 없고  
그렇게 하는 것이 훨씬 빠르기 때문에 밑의 코드를 짜보았다.
```python
n = int(input())
arr = []
for i in range(n):
    arr.append(list(map(int, input())))

def solve(x, y, n):
    if check(x, y, n):
        print(arr[x][y], end="")
    else:
        print("(", end="")
        for i in range(2):
            for j in range(2):
                solve(x+i*n//2, y+j*n//2, n//2)
        print(")", end="")

def check(x, y, n):
    for i in range(x, x+n):
        for j in range(y, y+n):
            if arr[x][y] != arr[i][j]:
                return False
    return True

solve(0, 0, n)
```

##### 두번째 풀이 - 5달 전
지금의 풀이와 비슷한 코드이다.  
차이점으로는 4부분을 각 좌표로 나누어 맨 왼쪽위 좌표, 맨 오른쪽아래 좌표를 분기로 설정 후,  
괄호를 append 해주는 형식으로 풀었었다.  
어짜피 이 4조건은 순서대로 실행되므로 굳이 넣어줄 필요없는 코드라고 생각한다.
```python
def isValid(x, y, n):
    for i in range(x, x+n):
        for j in range(y, y+n):
            if graph[x][y] != graph[i][j]:
                return False
    return True

def solve(x, y, n):
    if isValid(x, y, n):
        string.append(graph[x][y])
        return 
    
    half = n // 2
    for i in range(2):
        for j in range(2):
            if i == 0 and j == 0:
                string.append('(')
                solve(x+i*half, y+j*half, half)
            elif i == 1 and j == 1:
                solve(x+i*half, y+j*half, half)
                string.append(')')
            else:
                solve(x+i*half, y+j*half, half)

n = int(input())
graph = [list(map(int, input())) for _ in range(n)]
string = []
solve(0, 0, n)
for i in range(len(string)):
    print(string[i], end='')
```
#### 개선할 점 & 얻은 점
재귀를 이해할 수록 난이도가 점점 낮아지는 기분이다.  
재귀를 하나하나 함수에 빠져가면서 값을 도출하기 보다는  
컴퓨터를 믿고 이런 코드를 짜면 나머지는 똑같이 나올 것이다라는 확신만 가지고  
문제에 임하면 될 것 같다.