## BOJ 1003 피보나치 함수
#### 문제 접근 전략
피보나치수열 관련 문제이다.  
0값과 1값을 얼마나 호출하는지 계산하는 문제인데, 피보나치 수열의 재귀함수 특성상,  
기억으로 3~40을 넘어가면 엄청난량의 계산을 하게된다.(스택오버플로우가 발생할 수 있음).  
그러므로 한 수에 대한 0,1의 호출량은 정해져 있고 점화식을 이용하여 바텀업 형식을 사용하는  
DP알고리즘을 이용하기로 결정하였다.  

##### 첫번째 풀이 - 정답
0, 1의 호출량은 정해져 있으므로 보텀업 반복문을 사용해주었는데,  
0의 0호출량, 1의 1호출량을 미리 할당해준 뒤 2부터 40까지 계산을 해두었다.  
```python
dp = [[0, 0] for _ in range(41)]
dp[0][0] = 1
dp[1][1] = 1

for i in range(2, 41):
    dp[i][0] = dp[i-1][0] + dp[i-2][0]
    dp[i][1] = dp[i-1][1] + dp[i-2][1]
    
for _ in range(int(input())):
    print(*dp[int(input())])
```

##### 두번째 풀이 - 정답(7달전 풀이)
풀이 방법이야 똑같지만 확연히 메모리, 속도면에서 차이가 나는 것을 알 수 있었다.  
```python
import sys
input = sys.stdin.readline
result0 = [0] * 42
result1 = [0] * 42
for i in range(int(input())):
    n = int(input())
    def fibo(n):
        result0[0] = 1
        result1[1] = 1
        result0[2] = 1
        result0[3] = 1
        result1[2] = 1
        result1[3] = 2
        if n <= 3:
            print(result0[n], result1[n])
            return
        for i in range(4, n+1):
            result0[i] = result0[i-1] + result0[i-2]
            result1[i] = result1[i-1] + result1[i-2]
        print(result0[n], result1[n])
        return
    fibo(n)
```

#### 개선할 점 & 얻은 점
파이썬의 미숙함도 있었지만, 슈도코드의 부재가 문제를 어떻게 풀어나가야 하는지에  
차이가 있는 것 같다. 7달 전 풀이와 비교해 보면 난잡하지 않고 코드의 짜임새도 많이 개선되어  
있는 것으로 보인다. 슈도코드를 통해서 어떻게 코드를 써갈 것이고 문제 해결에 대한 통찰력을  
기를 수 있다고 생각하였다.