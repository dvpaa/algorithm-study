## BOJ 1107 리모컨

#### 문제 접근 전략
그리드 문제 같으면서도 모든 경우의 수를 탐색할 수 있는 시간복잡도가 가능해 브루트포스로 접근하면 되는 문제이다.

##### 첫번째 풀이 - 오답
여러 조건을 달아 보고 제출했지만 예외가 하나씩 있었고 결국 모든 중복 순열을 구해 자릿수와 차의 합이 가장 작은 것을 선택해주었다. 
```python
from itertools import product

n = int(input())
m = int(input())
nums = set(range(10))
if m > 0:
    nums = list(nums.difference(set(map(int, input().split()))))
def solve():
    if n == 100:
        return 0

    min_dif = int(1e9)
    for i in range(1, len(str(n))+1):
        for p in product(nums, repeat=i):
            tmp = int("".join(map(str, p)))
            tmp_val = abs(n - tmp) + len(str(tmp))
            if tmp_val < min_dif:
                min_dif = tmp_val

    return min(abs(n-100), abs(min_dif))

print(solve())
```

##### 두번째 풀이 - 다른 사람 풀이 참고
예외는 채널이 무제한이라는 것이다. target 값이 500,000이라면 +로 499,999번 가는 것과   
600,000에서 -로 100,000번 가는 여러 경우가 존재하기 때문에 추가적인 범위를 설정해주어야 한다.
```python
n = int(input())
m = int(input())
broken = list(map(int, input().split()))
min_count = abs(100 - n)
for nums in range(1000001):
    nums = str(nums)
    for j in range(len(nums)):
        if int(nums[j]) in broken:
            break
        elif j == len(nums) - 1:
            min_count = min(min_count, abs(int(nums) - n) + len(nums))
print(min_count)
```

#### 개선할 점 & 얻은 점
결국 예외는 문제에 있었다. 모든 중복 순열을 구해서 답을 처리하면 대부분 테스트 케이스는 맞겠지만  
500,000이상의 수에서 접근하는 방식이 최적의 해가 될 가능성이 존재하였다.  
접근하는 방식은 쉬웠지만 이러한 예외도 고려해야한다는 것을 깨달은 문제이다.