## 문제
https://school.programmers.co.kr/learn/courses/30/lessons/1845

## 풀이
### 설명
중복을 제거한 길이와 전체를 2로 나눈 몫중 최소값을 구하는 문제이다.

### python3 코드
```python
def solution(nums):
    return min(len(nums)//2, len(set(nums)))
```

### Java 코드
```java
import java.util.HashSet;

class Solution {
    public int solution(int[] nums) {
        HashSet<Integer> hashSet = new HashSet<>();
        for (int num: nums) {
            hashSet.add(num);
        }
        
        int defaultValue = nums.length / 2;
        int contrastValue = hashSet.size();
        return Math.min(defaultValue, contrastValue);
    }
}
```
