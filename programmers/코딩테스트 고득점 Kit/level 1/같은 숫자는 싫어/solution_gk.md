## 문제
https://school.programmers.co.kr/learn/courses/30/lessons/12906

## 풀이
### 설명
list에 이전 값과 비교해 값이 다를 경우에만 넣어 주었다.

스택개념을 이용해서 접근했다.

python의 경우 내장 자료형인 List, Java의 경우 ArrayList를 import해서 구현했다.


### python3 코드
```python3
def solution(arr):
    answer = [arr[0]]
    for num in arr[1:]:
        if answer[-1] != num:
            answer.append(num)
    return answer
```

### Java 코드
```java
import java.util.*;

public class Solution {
    public int[] solution(int []arr) {
        ArrayList<Integer> list = new ArrayList<>();
        int prevNum = 10;
        
        for (int num: arr) {
            if (prevNum != num) {
                list.add(num);
                prevNum = num;
            }
        }
        
        int size = list.size();
        int[] answer = new int[size];
        
        for (int i=0; i<size; i++) {
            answer[i] = list.get(i);
        }
        return answer;
    }
}
```
