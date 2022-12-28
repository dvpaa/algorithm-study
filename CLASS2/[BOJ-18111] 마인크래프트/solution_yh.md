## BOJ 18111 마인크래프트
#### 문제 접근 전략
브루트포스 문제로 보인다. 높이를 일정하게 맞추어야 하므로 배열을  
완전탐색이 필요해 보이고, 블럭의 개수가 한정되어 있기 때문에 블록을 쌓다가  
부족하면 윗 블럭을 때어서 가져오는 알고리즘도 구현해야 할 것으로 보인다.  


##### 첫번째 풀이 - 시간초과
풀이법은 생각한 대로 작성하였다. 그러나 코드를 짜면서 이 풀이는 틀릴 것이라고 생각하였다.  
왜냐하면 이 풀이는 현재 배열에 존재하는 블록의 높이만을 가질 수가 있어서 다른 높이의 정답이  
나올 수 없었기 때문이다. 
```python
import sys
input = sys.stdin.readline

# 세로 n, 가로 m, 맨 왼쪽 위의 좌표 (0, 0), 집터 내의 땅의 높이를 일정하게 바꾸기
n, m, b = map(int, input().split())
INF = int(1e9)
arr = []
for _ in range(n):
    for i in map(int, input().split()):
        arr.append(i)
arr.sort()

result = []
for i in range(n*m):
    tmp = arr[i]
    need_b, avl_b, tmp_t = 0, 0, 0
    for j in range(n*m):
        if arr[j] < tmp:    # 현재 높이보다 낮은 경우
            tmp_b = tmp - arr[j]  # 쌓기 위한 블록 수
            tmp_t += tmp_b         # 필요한 시간
            need_b += tmp_b
        elif arr[j] > tmp:
            tmp_b = arr[j] - tmp   # 인벤토리에 넣어지는 블록 수
            tmp_t += 2*tmp_b        # 필요한 시간
            avl_b += tmp_b

    if b + avl_b - need_b < 0:
        result.append((INF, -1))
    else:
        result.append((tmp_t, tmp))

result.sort(key=lambda x:(x[0], -x[1]))
print(result[0][0], result[0][1])
```

##### 두번째 풀이 - 통과(pypy)
게시판의 일부 코드를 참고하였다.  
단순한 생각을 하지 못했었다. 어짜피 최솟값과 최댓값의 높이 차 내에서만  
높이는 구성되므로 차만큼 하나씩 돌면 끝이었다.  
나머지 풀이는 바꿀게 없어서 그대로 두었다.
```python
import sys
input = sys.stdin.readline

# 세로 n, 가로 m, 맨 왼쪽 위의 좌표 (0, 0), 집터 내의 땅의 높이를 일정하게 바꾸기
n, m, b = map(int, input().split())
INF = int(1e9)
arr = []
for _ in range(n):
    for i in map(int, input().split()):
        arr.append(i)
arr.sort()
min_val, max_val = arr[0], arr[-1]
result = []
for i in range(min_val, max_val+1):
    need_b, avl_b, tmp_t = 0, 0, 0
    for j in arr:
        if j < i:    
            tmp_b = i - j  # 쌓기 위한 블록 수
            tmp_t += tmp_b         # 필요한 시간
            need_b += tmp_b
        elif j > i:
            tmp_b = j - i   # 인벤토리에 넣어지는 블록 수
            tmp_t += 2*tmp_b        # 필요한 시간
            avl_b += tmp_b

    if b + avl_b - need_b < 0:
        result.append((INF, -1))
    else:
        result.append((tmp_t, i))

result.sort(key=lambda x:(x[0], -x[1]))
print(result[0][0], result[0][1])
```

#### 개선할 점 & 얻은 점
문제 해결하는데에 시간이 조금 소요되었다. 코드 작성에 앞서서 아이디어를 짜는데 시간이 걸렸었다.  
문제의 핵심은 파악했지만 사소한 한 부분에서 생각을 하지 못하였다.  
문제를 해결하기 위해선 어떤 알고리즘이 적용되는지 파악을 하는 것이 열쇠가 되는 것을 느꼈다.