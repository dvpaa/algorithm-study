## 문제
https://school.programmers.co.kr/learn/courses/30/lessons/42578

## 풀이
### 설명
옷 종류별 개수를 각각 1씩더해서 곱한 후 마지막에 -1 해주었다.

### python3 코드
```python3
def solution(clothes):
    cloth_type = dict()
    for cloth in clothes:
        cloth_type.setdefault(cloth[1], 0)
        cloth_type[cloth[1]] += 1
    
    result = 1
    for num in cloth_type.values():
        result *= (num+1)
    
    return result-1
```

### Java
```java
import java.util.Map;
import java.util.HashMap;

class Solution {
    public int solution(String[][] clothes) {
        Map<String, Integer> map = new HashMap<String, Integer>();
        
        for (String[] cloth: clothes) {
            map.put(cloth[1], map.getOrDefault(cloth[1], 0) + 1);
        }
        
        int result = 1;
        for (Integer num: map.values()) {
            result *= (num+1);
        }
        return result-1;
    }
}
```
