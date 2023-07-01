## BOJ 9465 스티커

#### 문제 접근 전략
dp문제이다. 2*n타일링 + 누적합을 더한 문제로 보인다.

##### 첫번째 풀이 - 오답
생각이 너무 많은 풀이였다. 일반화를 하지 못해 점화식을 구체적으로 쓰지 못한 점이 오답의 가장 큰 요인이었다.  
테스트케이스는 전부 통과했지만 풀면서도 아 이건 틀릴 것 같다라고 생각이 들었었다.  
dp[i]는 d[i-1] + 선택할 수 있는 항과 d[i-2]+data[i]의 최댓값을 이용하여 풀었다.
```python
for _ in range(int(input())):
    n = int(input())
    dp = [0]*n
    data = [list(map(int, input().split())) for _ in range(2)]
    row = [0]*n

    if data[0][0] >= data[1][0]:
        row[0] = 0
    else:
        row[0] = 1
    dp[0] = data[row[0]][0]

    if n >= 2:
        if data[0][0] + data[1][1] >= data[1][0] + data[0][1]:
            row[1] = 1
            dp[1] = data[0][0] + data[1][1]
        else:
            row[1] = 0
            dp[0] = data[1][0] + data[0][1]

        for i in range(2, n):
            if row[i-1] == 1: # 선택할 수 있는 행
                canUse = 0
            else:
                canUse = 1

            if data[0][i] >= data[1][i]:
                maximum = 0
            else:
                maximum = 1

            first = dp[i-1]+data[canUse][i]
            second = dp[i-2]+data[maximum][i]

            if first >= second:
                dp[i] = first
                row[i] = canUse
            else:
                dp[i] = second
                row[i] = maximum

    print(dp[n-1])
```

##### 두번째 풀이 - 다른 사람 풀이 참고
누적합으로 계산해가며 푼 풀이이다.  
i번째 dp의 첫번째 행이 최댓값이 되려면 i-1번째 dp의 두번째 행과 i-2번째 dp의 두번째 행 둘 중에서 더 큰 값을 선택하는 경우 2가지가 있다.
```python
for _ in range(int(input())):
    n = int(input())
    dp = [list(map(int, input().split())) for _ in range(2)]
    if n>=2:
        dp[0][1] += dp[1][0]
        dp[1][1] += dp[0][0]
        for i in range(2, n):
            dp[0][i] += max(dp[1][i-1], dp[1][i-2])
            dp[1][i] += max(dp[0][i-1], dp[0][i-2])
    print(max(dp[0][n-1], dp[1][n-1]))
```

#### 개선할 점 & 얻은 점
dp를 선언 시에 꼭 1차원으로 하지 않는 테크닉을 배울 수 있었다. 점화식을 세우는 것에 집중하자. 