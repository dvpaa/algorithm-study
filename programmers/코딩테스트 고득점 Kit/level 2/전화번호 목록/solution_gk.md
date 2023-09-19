## 문제
https://school.programmers.co.kr/learn/courses/30/lessons/42577

## 풀이
### 설명
모든 전화번호들을 딕셔너리(자바의 경우 Map)의 key로 넣어놓고 모든 문자열들을 비교했다.

### python3 코드
```python3
def solution(phone_book):
    book = {key: 0 for key in phone_book}
    for num in phone_book:
        for i in range(1, len(num)):
            if num[:i] in book:
                return False
    return True
```

### Java 코드
```java
import java.util.HashMap;
import java.util.Map;


class Solution {
    public boolean solution(String[] phoneBook) {

        Map<String, Integer> map = new HashMap<>();

        for(int i = 0; i < phoneBook.length; i++) {
            map.put(phoneBook[i], i);
        }


        for(int i = 0; i < phoneBook.length; i++) {
            for(int j = 0; j < phoneBook[i].length(); j++) {
                if(map.containsKey(phoneBook[i].substring(0,j))) {
                    return false;
                }
            }
        }

        return true;
    }
}
```
