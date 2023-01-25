## 문제
https://school.programmers.co.kr/learn/courses/30/lessons/42586

## 풀이
### 설명
순차적으로 필요한 일수와 현재를 비교하여 조건을 나눠주었다.

Java의 경우 같은 로직으로 풀었다가 다른 사람의 풀이를 참고했다.


### python3 코드
```python3
import math

def solution(progresses, speeds):
    answer = []
    day = calculate_day(progresses[0], speeds[0])
    cnt = 0
    for progress, speed in zip(progresses, speeds):
        required_day = calculate_day(progress, speed)

        if day >= required_day:
            cnt += 1
        else:
            answer.append(cnt)
            cnt = 1
            day = required_day
            
    answer.append(cnt)
    return answer


def calculate_day(progress, speed):
    return math.ceil((100-progress) / speed)
```

### Java 코드
```java
import java.util.Arrays;

class Solution {
    
    public int[] solution(int[] progresses, int[] speeds) {
        int[] dayOfend = new int[100];
        int day = -1;
        
        for(int i=0; i<progresses.length; i++) {
            while(progresses[i] + (day*speeds[i]) < 100) {
                day++;
            }
            dayOfend[day]++;
        }
        return Arrays.stream(dayOfend).filter(i -> i!=0).toArray();
    }
}
```
