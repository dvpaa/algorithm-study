## BOJ 15829 Hashing

#### 문제 접근 전략
해시함수를 이용한 문제이다. 알파벳을 수로 치환하여 더하고 출력하기만 하면 됨. 오버플로우를 방지하기 위해서 모듈로 연산을 이용해주면 됨.

##### 첫번째 풀이 - 정답
각 알파벳의 순서를 사전형으로 만들어 주었고 해시함수를 적용하여 풀이.
```python
n = int(input())
s = list(input())
alphabet = dict()
for i in range(1, 27):
    alphabet[chr(96+i)] = i
result = 0
for i in range(n):
    result += alphabet[s[i]]*(31**i)
print(result % 1234567891)
```

#### 개선할 점 & 얻은 점
해시함수를 응용할 수 있는 초급문제이다. 오버플로우에 관해 더 신경쓰게 되었다.