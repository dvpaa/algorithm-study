## BOJ 1259 팰린드롬수

#### *문제 접근 전략
특별한 조건이 없이 숫자를 뒤집었을 때 같은 수를 찾는 문제  
단순한 생각보다 투포인터로 접근하였음.

##### 첫번째 풀이 - 정답
수를 절반으로 나누고 접근해보는 등 여러 시도가 있었지만 투포인터로 접근하는 것이  
가장 빠르고 쉽게 구현할 수 있다고 느낌.
```python
while True:
    try:
        num = list(input())
        if num[0] == '0': 
            break

        l, r = 0, len(num)-1
        is_avl = True
        while l < r:
            if num[l] != num[r]:
                is_avl=False
                break
            l += 1
            r -= 1

        print('yes') if is_avl else print('no')

    except EOFError:
        break
```

##### 두번째 풀이 - 다른 사람 풀이 참고
슬라이싱을 이용하여서 접근할 수 있다는 것을 참고하게 됨.
```python
while True:
    num = input()
    if num == '0': break

    if num[::-1] == num:
        print('yes')
    else:
        print('no')
```

#### 개선할 점 & 얻은 점
두번째 풀이에서 슬라이싱 개념보다 연산자의 개념에 문제가 있었음.  
비교연산자(==)는 Object의 Value를 비교하기 때문에 객체의 id비교가 아니라서  
그냥 전환 후 비교만 해주면 됨.  
물론 num[::-1]과 num의 id는 같겠지만 헷갈렸던 부분을 명확하게 할 수 있게된 점.