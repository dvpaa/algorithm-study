## 문제
https://school.programmers.co.kr/learn/courses/30/lessons/42576

## 풀이
### 설명
참가자에 동명이이인이 있을 수 있어 딕셔너리(Java의 경우 Map)에 참가자 이름을 key, 이름에 대한 사람 수를 value로 저장했다.

다음으로 완주한 사람의 value를 -1해주어 최종적으로 0이 아닌 value를 가진 key를 찾았다.

옛날에 이 문제를 정렬로 풀었었는데 사전 자료형을 이용해서 O(N)으로 접근했다.

### python3 코드
```python3
def solution(participant, completion):
    people_dict = dict()
    for person in participant:
        people_dict.setdefault(person, 0)
        people_dict[person] += 1
    
    for person in completion:
        people_dict[person] -= 1
    
    for key, val in people_dict.items():
        if val != 0:
            return key
```

### Java 코드
```java
import java.util.*;

class Solution {
    public String solution(String[] participant, String[] completion) {
        HashMap<String, Integer> hashMap = new HashMap<String, Integer>();
        String answer = "";
        
        for (String person: participant) {
            int val = hashMap.getOrDefault(person, 0);
            hashMap.put(person, val+1);
        }
        
        for (String person: completion) {
            hashMap.put(person, hashMap.get(person) - 1);
        }
        
        for (Map.Entry<String, Integer> entry: hashMap.entrySet()) {
            if (entry.getValue() != 0) {
                answer = entry.getKey();
                break;
            }
        }
        return answer;
    }
}
```
