## 문제
https://school.programmers.co.kr/learn/courses/30/lessons/42748

## 풀이
### 설명
각 배열을 슬라이싱하여 정렬후 원하는 인덱스의 값을 찾아내는 된다.

Java의 경우 슬라이싱 메서드를 따로 구현했는데 `Arrays.copyOfRange()`메서드의 존재를 다 풀고 알았다.


### python3 코드
```python3
def solution(array, commands):
    result = []
    for command in commands:
        arr = sorted(array[command[0]-1:command[1]])
        result.append(arr[command[2]-1])
    return result
```


### Java 코드
```java
import java.util.*;

class Solution {
    public int[] solution(int[] array, int[][] commands) {
        int[] answer = new int[commands.length];
        
        for (int i=0; i<commands.length; i++) {
            int start = commands[i][0];
            int end = commands[i][1];
            int k = commands[i][2];
            
            int[] slicingArray = getSliceOfArray(array, start, end);
            Arrays.sort(slicingArray);
            
            answer[i] = slicingArray[k-1];
        }
        return answer;
        
        
    }
    
    private int[] getSliceOfArray(int[] array, int start, int end) {
        final int size = end-start+1;
        int[] slicingArray = new int[size];
        for (int i=start-1; i<end; i++) {
            slicingArray[i-(start-1)] = array[i];
        }
        return slicingArray;
    }
}
```
