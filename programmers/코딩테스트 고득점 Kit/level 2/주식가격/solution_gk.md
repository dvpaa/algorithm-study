## 문제
https://school.programmers.co.kr/learn/courses/30/lessons/42584

## 풀이
### 설명
스택에 현재의 시간과 가격을 최상단 원소와 비교해가면 삽입하고 추출해주었다.

현재 시간 - 추출한 원소의 시간을 해당원소의 떨어지지 않은 기간으로 기록했다.

### python3 코드
```python3
def solution(prices):
    answer = [0] * len(prices)
    stack = [(0, prices[0])]
    
    for time in range(1, len(prices)):
        while stack:
            if stack[-1][1] > prices[time]:
                prev_time, prev_price = stack.pop()
                answer[prev_time] = time - prev_time
            else:
                break
        stack.append((time, prices[time]))

    top_time, top_price = stack.pop()
    while stack:
        time, price = stack.pop()
        answer[time] = top_time - time
    
    return answer
```

### Java 코드
```java
import java.util.Stack;
import java.util.List;
import java.util.ArrayList;
import java.util.Arrays;

class Solution {
    public int[] solution(int[] prices) {
        int[] answer = new int[prices.length];
        Stack<List<Integer>> stack = new Stack<>();
        stack.push(new ArrayList<Integer>(Arrays.asList(0, prices[0])));

        for (int i=1; i<prices.length; i++) {
            while (!stack.empty()) {
                if (stack.peek().get(1) > prices[i]) {
                    List<Integer> list = stack.pop();
                    answer[list.get(0)] = i - list.get(0);
                }
                else { break; }
            }
            stack.push(new ArrayList<Integer>(Arrays.asList(i, prices[i])));
        }

        int topTime = stack.pop().get(0);
        while (!stack.empty()) {
            int time = stack.pop().get(0);
            answer[time] = topTime - time;
        }

        return answer;
    }
}
```
