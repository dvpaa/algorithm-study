## BOJ 1018 체스판 다시 칠하기

#### *문제 접근 전략
다양한 사이즈의 보드 중 일부분(8x8 크기)만 슬라이싱을 통하여 접근  
정답 체스판은 존재하기에 두개의 체스판을 만든 뒤 부분 보드와 체스판을 비교하여  
다른 개수가 더 적은 것을 해당 부분 보드의 다시 칠해야 하는 정사각형의 최소 개수로 지정.

##### 첫번쨰 풀이 - 예제는 모두 정답

부분 보드의 각 열에 대해서 흑,백의 개수 차이의 절반 만큼이 바꾸어줘야 하는 개수임을 인지함.  
어떠한 경우의 수에도 "BWBWBWBW" or "WBWBWBWB".  

즉, 정답 체스판의 B의 개수와 W의 개수는 정해져 있고 그 차이의 절반 만큼이 바꾸어 주어야 하는 것으로 판단하고 코드를 작성함.
``` python
def check(a, x, y):
    chess = [row[y:y+8] for row in a[x:x+8]]
    change = 0
    for i in range(8):
        change += abs(chess[i].count("B") - chess[i].count("W")) // 2
    return change

m, n = map(int, input().split())
arr = []
for _ in range(m):
    arr.append(list(input()))

result = []
for i in range(m-7):
    for j in range(n-7):
        result.append(check(arr, i, j))
print(min(result))
```

##### 두번째 풀이 - 정답

첫번째 풀이의 반례가 떠오르지 않아 질문 게시판의 반례 참고.  
반례는 "WWBWBWBB" 같은 경우 개수는 동일하지만 주변 색과는 달라야 한다는 정의에 모순.  
그렇다면 어짜피 정답체스판은 존재하므로 두 경우의 수인 체스판을 만들고,  
두 체스판과 부분 보드와의 다른 개수 중 최소 값을 해당 부분 보드의 칠해야 하는 정사각형의 개수로 지정.
```python
def check(a, x, y):
    chess = [row[y:y+8] for row in a[x:x+8]]
    
    board1, board2 = make_board()
    
    change1 = 0
    for i in range(8):
        for j in range(8):
            if chess[i][j] != board1[i][j]:
                change1 += 1
    
    change2 = 0
    for i in range(8):
        for j in range(8):
            if chess[i][j] != board2[i][j]:
                change2 += 1

    return min(change1, change2)

def make_board():
    row1 = 'BWBWBWBW'
    row2 = 'WBWBWBWB'
    board1 = []
    board2 = []
    for _ in range(4):
        board1.append(list(row1))
        board1.append(list(row2))

    for _ in range(4):
        board2.append(list(row2))
        board2.append(list(row1))

    return board1, board2

m, n = map(int, input().split())
arr = []
for _ in range(m):
    arr.append(list(input()))

result = []
for i in range(m-7):
    for j in range(n-7):
        result.append(check(arr, i, j))
print(min(result))
```

##### 세번째 풀이 - 다른 사람 코드 참고
두번째 풀이가 너무 하드 코딩이었다고 생각하고 리팩토링을 시도,  
더이상 떠오르지가 않아서 정답 코드를 참고하여 부분 리팩토링.  
정답 코드는 각 체스판의 색깔이 위치마다 정해져 있으므로 인덱싱을 통해 최소값을 결정함  
전체적인 구상은 비슷하지만 코드의 간결성과 속도면에서의 감소가 더 좋은 효율을 보인 코드임.  
굳이 함수로 빼서 슬라이싱으로 메모리를 차지하긴 하지만 코드 이해도 면에서는 더 낫다고 판단하여 밑처럼 작성하였음.
```python
def check(board, x, y):
    chess = [row[y:y+8] for row in board[x:x+8]]
    
    change1, change2 = 0, 0    # 1은 W칸일 시, 2는 B칸일 시
    for i in range(8):
        for j in range(8):
            if (i+j) % 2 == 0: # 짝수 칸
                if chess[i][j] != 'W':
                    change1 += 1
                if chess[i][j] != 'B':
                    change2 += 1
            else:              # 홀수 칸
                if chess[i][j] != 'B':
                    change1 += 1
                if chess[i][j] != 'W':
                    change2 += 1

    return min(change1, change2)

m, n = map(int, input().split())
arr = []
for _ in range(m):
    arr.append(list(input()))

result = []
for i in range(m-7):
    for j in range(n-7):
        result.append(check(arr, i, j))
print(min(result)) 
```

#### 개선할 점 & 얻은 점
풀이하는 과정에서 2차원 리스트 슬라이싱에 대한 기술적 부족함이 있었음.  
다른 문제에서 이러한 스킬을 사용할 때에 도움이 될 것으로 기대.  
모든 곳을 탐색하는 브루트포스 문제인 만큼 문제 상의 몇 가지 조건이 해당 문제 풀이의 '키'임을 다시 한 번 상기할 수 있었던 문제.