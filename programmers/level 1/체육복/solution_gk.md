## 문제
https://school.programmers.co.kr/learn/courses/30/lessons/42862


## 풀이
### 설명
체육복을 잃어버린 학생들을 차례대로 접근하면서 우선적으로 앞에서 없으면 뒤에서 채우는 방식으로 풀었다.

다만, 잃어버린 학생과 여분이 있는 학생이 동시에 존재할 수 있음을 고려해야한다.

때문에 시간과 공간에서 더 효율적으로 접근하기위해 미리 students 배열을 초기화 시키고 lost와 reserve를 순회하며 각각 students의 초깃값을 설정해줬다.

python에서는 리스트를 원하는 값으로 초기화할 수 있는 반면에 Java에서는 0으로 초기화 되어 Java코드는 0을 기준으로 -1, +1 해주었다.

또한, 배열을 n+2 크기로 초기화시켜 앞과 뒤의 범위에 대한 조건을 고려하지않게 만들었다


### python3 코드
```python3
def solution(n, lost, reserve):
    students = [-1] + [1] * n + [-1]
    for l in lost:
        students[l] -= 1
    for r in reserve:
        students[r] += 1
    
    cnt = 0
    
    for idx in range(1, n+1):
        if students[idx] == 0:
            prev_idx = idx - 1
            next_idx = idx + 1
            
            if students[prev_idx] == 2:
                students[prev_idx] -= 1
                students[idx] += 1
                
            elif students[next_idx] == 2:
                students[next_idx] -= 1
                students[idx] += 1
            
    return count_answer(students)


def count_answer(students: list) -> int:
    cnt = 0
    for student in students:
        if student >= 1:
            cnt += 1
    return cnt
```


### Java 코드
```java
import java.util.*;

class Solution {
    public int solution(int n, int[] lost, int[] reserve) {
        int[] students = new int[n+2];
        students[0] = -2;
        students[n+1] = -2;
        
        for (int lostIdx: lost) {
            students[lostIdx] -= 1;
        }
        for (int reserveIdx: reserve) {
            students[reserveIdx] += 1;
        }
        
        for (int i=1; i<n+1; i++) {
            if (students[i] == -1) {
                int prevIdx = i - 1;
                int nextIdx = i + 1;
                
                if (students[prevIdx] == 1) {
                    students[i] += 1;
                    students[prevIdx] -= 1;
                }
                else if (students[nextIdx] == 1) {
                    students[i] += 1;
                    students[nextIdx] -= 1;
                }
            }
        }
        
        return countAnswer(students);
        
    }
    
    
    private int countAnswer(int[] students) {
        int cnt = 0;
        for (int val: students) {
            if (val >= 0) {cnt+=1;}
        }
        return cnt;
    }
}
```
