## 문제
https://school.programmers.co.kr/learn/courses/30/lessons/42840

## 풀이
### 설명
각 답안별 점수를 매겨서 최대값들의 인덱스를 뽑아내는 방식으로 풀었다.

코드를 짧게 작성하기보다는 기능별로 함수를 뽑아내고 가독성이 높아지도록 작성했다.

### python3 코드
```python3
def solution(answers):
    solutions = [[1, 2, 3, 4, 5], 
                 [2, 1, 2, 3, 2, 4, 2, 5], 
                 [3, 3, 1, 1, 2, 2, 4, 4, 5, 5]]
    
    scores = [get_score(answers, solution) for solution in solutions]
    return get_max_idx_list(scores)
    

def get_score(answers: list, solution: list) -> int:
    size = len(solution)
    score = 0
    idx = 0
    
    for answer in answers:
        if solution[idx] == answer:
            score += 1
        idx = (idx+1) % size
    
    return score


def get_max_idx_list(array: list) -> list:
    max_val = max(array)
    return [idx+1 for idx, val in enumerate(array) if val == max_val]
```

### Java 코드
```java
import java.util.*;

class Solution {
    public int[] solution(int[] answers) {
        int[][] solutions = {
            {1, 2, 3, 4, 5},
            {2, 1, 2, 3, 2, 4, 2, 5},
            {3, 3, 1, 1, 2, 2, 4, 4, 5, 5}
        };
        int size = solutions.length;
        int[] scores = new int[size];
        
        for (int i=0; i<size; i++) {
            scores[i] = getScore(answers, solutions[i]);
        }
        return getMaxIdxArr(scores);
        
        
    }
    
    private int getScore(int[] answers, int[] solution) {
        int idx = 0;
        int score = 0;
        int size = solution.length;
        
        for (int answer: answers) {
            if (answer == solution[idx]) { score++; }
            idx = (idx+1) % size;
        }
        return score;
    }
    
    private int[] getMaxIdxArr(int[] array) {
        int maxVal = getMaxValue(array);
        int size = array.length;
        ArrayList<Integer> list = new ArrayList<>();
        
        for (int i=0; i<size; i++) {
            if (array[i] == maxVal) { list.add(i+1); }
        }
        return list.stream().mapToInt(i->i.intValue()).toArray();
        
    }
    
    private int getMaxValue(int[] array) {
        int maxVal = -1;
        for (int num: array) {
            maxVal = Math.max(maxVal, num);
        }
        return maxVal;
    }
}
```
