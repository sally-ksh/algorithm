
### [타켓넘버](https://school.programmers.co.kr/learn/courses/30/lessons/43165)

## 😃 개인 풀이

- 자료구조 : 그래프
- 시간 복잡도 : O(2^n), 공간복잡도 : O(1)

``` java
import java.util.*;

class Solution {
    int answer = 0;
 
    public int solution(int[] numbers, int target) {
        dfs(0, 0, numbers, target);
        return answer;
    }
    
    private void dfs(int sum, int idx, int[] numbers, int target){
        if(idx == numbers.length){
            if(sum == target) answer++;
        } else {
            dfs(sum - numbers[idx], idx+1, numbers, target);  // O(n)
            dfs(sum + numbers[idx], idx+1, numbers, target);  // O(n)
        }
    }
}
```
