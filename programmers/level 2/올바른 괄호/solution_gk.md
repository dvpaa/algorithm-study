## 문제
https://school.programmers.co.kr/learn/courses/30/lessons/12909

## 풀이
### 설명
스택 자료구조를 이용해서 '('일 경우 push ')'일 경우 pop 연산을 진행하고 최후에 스택이 비었는지 검사한다.

### python3 코드
```python3
def solution(s):
    stack = []
    for element in s:
        if element == '(':
            stack.append(element)
        else:
            if not stack:
                return False
            stack.pop()
    
    return False if stack else True
```

### Java 코드
```java
import java.util.Stack;

class Solution {
    boolean solution(String s) {
        int length = s.length();
        Stack<String> stack = new Stack<>();
        
        for (int i=0; i<length; i++) {
            if (s.charAt(i) == ')') {
                if (stack.empty()) { return false; }
                stack.pop();
            }
            else {
                stack.push("(");
            }
        }
        if (stack.empty()) { return true; }
        else { return false; }
    }
}
```
