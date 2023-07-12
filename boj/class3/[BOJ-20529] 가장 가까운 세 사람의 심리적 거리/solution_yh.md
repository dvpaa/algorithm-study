## BOJ 20529 가장 가까운 세 사람의 심리적 거리

#### 문제 접근 전략
mbti의 종류는 16가지로 n이 32까지는 2개씩 중복하여 여러 경우의 수가 나타날 수 있지만, 33부터 하나의 mbti는 무조건 3개가 되야 하므로  
그 이상의 수에 대해서는 의미가 없어져 가장 가까운 심리 거리의 수는 0이 된다. 32이하의 경우의 수에 대해서는 브루트포스를 이용해준다.

##### 첫번째 풀이 - 정답
```python
for _ in range(int(input())):
    n = int(input())
    data = list(input().split(" "))
    result = []
    if n > 32:
        print(0)
    else:
        for i in range(n):
            for j in range(i+1, n):
                for k in range(j+1, n):
                    count = 0
                    for s in range(4):
                        if data[i][s] != data[j][s]:
                            count += 1
                        if data[j][s] != data[k][s]:
                            count += 1
                        if data[k][s] != data[i][s]:
                            count += 1
                    result.append(count)
        print(min(result))
```
#### 개선할 점 & 얻은 점
찾아보니까 비둘기집 원리를 적용하여 푸는 문제라고 한다.  
> 비둘기집 원리  
> (n+1)개의 물건을 n개의 상자에 넣을 때 적어도 어느 한 상자에는 두 개 이상의 물건이 들어 있다  

즉, 16가지 mbti가 있을 때, k(k>16)명이 있으면 적어도 같은 mbti를 가지는 사람은 반드시 2명 이상이다.  
그렇다면 k(k>32)명이 있으면 적어도 같은 mbti를 가지는 사람은 반드시 3명 이상이므로, 0으로 처리해주면 되는 간단한 문제이다.