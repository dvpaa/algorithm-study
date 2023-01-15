## BOJ 1074 Z
#### 문제 접근 전략
4개의 사각형의 재귀 조건은 찾는 것이 주 목표이다.  
1->2->3->4 순으로 순서는 정해져있으며,  
N = k일 때의 결과가 N = k+1일 때의 결과에 영향을 미친다.  
좌표가 1,2,3,4 어느 사각형에 위치해 있냐에 따라서 k-1크기의 사각형을 다르게 더해주고 재귀를 실행한다.
##### 첫번째 풀이 - 풀이 참고
k 크기 사각형에서 k-1 크기 사각형으로 재귀를 할 때,  
좌표를 k-1 사각형으로 옮겨주며 각 m번 사각형 마다 다르게 크기제곱만큼 더해주었다.
```python
def solve(x, y, n): # 2^n x 2^n 배열에서 (r,c)를 방문하는 순서를 반환
    if n == 0:
        return 0
    half = 2**(n-1)
    if x < half and y < half:    # 1번 사각형
        return solve(x, y, n-1)
    elif x < half and y >= half: # 2번 사각형
        return half*half + solve(x, y-half, n-1)
    elif x >= half and y < half: # 3번 사각형
        return 2*half*half + solve(x-half, y, n-1)
    else:                        # 4번 사각형
        return 3*half*half + solve(x-half, y-half, n-1)

n, r, c = map(int, input().split())
print(solve(r, c, n))
```
#### 개선할 점 & 얻은 점
굉장히 어려운 문제였다. 재귀가 이해가 된 줄 알았지만 조금 더 점화식의 관점을 잘 보아야할 것 같다.  
코드는 바킹독 풀이를 참고했으며 한번 더 강의를 봐서 더 이해를 해야할 것 같다.