## BOJ 2579 계단오르기
#### 문제 접근 전략
조건에 따른 다이나믹 프로그래밍 문제이다.  
마지막 계단은 꼭 밟아야 하므로 두 가지 조건이 발생하는데,  
한 계단 전을 밟은 경우, 두 계단 전을 밟은 경우.  
1) 한 계단일 경우, 이 전 스텝은 두 칸이 차이가 나야하므로 마지막 계단의 합은  
i-3번째 dp값 + i-1번째 계단원소값 + i번째 계단원소값을 더한 값으로 된다.  
2) 두 계단일 경우, 이 전 스텝은 상관이 없으므로 마지막 계단의 합은  
i-2번째 dp값 + i번째 계단원소값을 더한 값이 된다.
##### 첫번째 풀이 - 정답
index error 때문에 초기화에 유의하여  
미리 최대 원소개수만큼 리스트를 만들어 주었다.
```python
import sys

n = int(input())
arr = [0]*301
dp = [0]*301
for i in range(n):
    arr[i] = int(sys.stdin.readline())
dp[0] = arr[0]
dp[1] = arr[0]+arr[1]
dp[2] = max(arr[0]+arr[2], arr[1]+arr[2])
for i in range(3, n):
    dp[i] = max(dp[i-3]+arr[i-1]+arr[i], dp[i-2]+arr[i])
print(dp[n-1])
```
##### 두번째 풀이 - 다른 사람 코드
조금 된 코드이다.  
이때의 테스트케이스로는 통과하였겠지만 인덱스를 고려하지않은 풀이이다.  
```python
import sys
input = sys.stdin.readline
arr = []
dp = []

l = int(input())
for _ in range(l):
    arr.append(int(input()))

dp.append(arr[0])
dp.append(max(arr[0]+arr[1],arr[1]))
dp.append(max(arr[0]+arr[2],arr[1]+arr[2]))
for i in range(3,l):
    dp.append(max(dp[i-2] + arr[i] , dp[i-3] + arr[i] + arr[i - 1]))

print(dp.pop())
```
#### 개선할 점 & 얻은 점
생각을 좀 많이해야했던 문제이다.  
두 칸 전 계단의 조건을 빠르게 파악하지 못한 것이 가장 큰 걸림돌이었다.  
두번재 풀이에서 얻은게 있었는데, 파이썬 리스트 자료구조의 장점을 살린 코드였다.  
리스트는 append 또는 pop시에 O(1)의 시간복잡도를 가지므로 초기화하지 않고 append하는 식,  
마지막 값 출력 시 pop을 이용한 마지막 계단 출력.  
테스트케이스가 많은 문제일 수록 O(n)의 시간을 도는 양이 많아지기 때문에  
이렇한 연산을 이용하는 것도 좋을 것 같다.