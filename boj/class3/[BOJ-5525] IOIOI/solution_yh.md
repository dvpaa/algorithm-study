## BOJ 5525 IOIOI

#### 문제 접근 전략
문자열을 이용한 문제이다.  
데이터의 개수가 100만개이므로 O(N)의 시간으로 끝낼 수 있는 알고리즘을 이용해 풀이해야할 것으로 보인다.
##### 첫번째 풀이 - 4프로 오답
첫번째 풀이는 투포인터를 이용하였다. end값을 기준으로 O(N)의 시간복잡도로 순회하기 때문에 시간 초과문제는 없어보이지만, WA를 받았다.
```python
n = int(input())
m = int(input())
s = input()
start, end = 0, 1
count = 0
result = 0
while end < len(s):
    # start 포인터가 I를 가르킬 때까지 이동
    if s[start] == 'O':
        start += 1
        end += 1
    else:
        # end 포인터가 가르키는 값과 이전 값이 같은 경우 하나씩 증가 ex) II
        if s[end] == s[end-1]:
            start += 1
            end += 1
        else:
            # 교차하는 경우 교차 카운트 1 증가 및 end point 이동
            count += 1
            # 교차 횟수가 n의 2배일 시 문자열이 속한 것이므로 개수 증가 및 start 이동, end start+1로 이동
            if count == 2*n:
                result += 1
                count = 0
                start += 1
                end = start+1
            else:
                end += 1

print(result)
```

##### 두번째 풀이 - 정답
IOI라는 패턴을 포인터를 활용하여 푼 코드이다. 인덱스 문제로 범위를 -1, now, +1로 두었다.  
now, +1, +2로 접근하였을 때 나머지 로직은 같지만 경우에 따라 인덱싱 문제가 발생할 수 있기 때문이다.  
패턴이 발생했을 때 0으로 초기화하지않고 -1을 하는 이유는 그 다음 패턴이 또 발생한다면 기존 IOI를 하나 빼고 추가하는 방식이 옳기 때문이다.
```python
n = int(input())
m = int(input())
S = input()
pointer = 1
pattern = 0
count = 0
while pointer < (m-1):
    if S[pointer-1] == 'I' and S[pointer] == 'O' and S[pointer+1] == 'I':
        pointer += 2
        pattern += 1
    else:
        pointer += 1
        pattern = 0
    if pattern == n:
        count += 1
        pattern -= 1

print(count)
```
##### 개선할 점 & 얻은 점
다양한 풀이로 풀 수 있는 문자열 문제이다. 생각보다 까다로웠지만, 인덱싱문제와 로직만 잘 구현하면 쉽게 통과할 수 있다. 