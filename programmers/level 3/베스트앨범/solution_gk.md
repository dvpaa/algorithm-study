## 문제
https://school.programmers.co.kr/learn/courses/30/lessons/42579

## 풀이
### python3 코드
```python3
def solution(genres, plays):
    answer = []
    total_plays = {}
    plays_idx = {}
    
    for idx, genre in enumerate(genres):
        total_plays[genre] = total_plays.setdefault(genre, 0) + plays[idx]
        
        if genre not in plays_idx:
            plays_idx[genre] = []
        
        plays_idx[genre].append((idx, plays[idx]))
        
    
    total_plays = sorted(list(total_plays.items()), key=lambda x: -x[1])
    
    for genre in total_plays:
        idx_list = sorted(plays_idx[genre[0]], key=lambda x: -x[1])
        if len(idx_list) == 1:
            answer.append(idx_list[0][0])
        else:
            for i in range(2):
                answer.append(idx_list[i][0])
    
    return answer
```
