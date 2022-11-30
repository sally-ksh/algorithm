
## 프로그래머스 - 네트워크

- [네트워크](https://school.programmers.co.kr/tryouts/46831/challenges)

### 😃 개인 풀이

재귀는 시간복잡도 계산이 쉽지 않고, 감으로 풀 때가 많아서 좀더 이해하며 풀고 싶습니다. 

- 자료구조 : DFS
- 시간복잡도 : O(n), 공간복잡도 : O(n)
- 풀이시간 : 1시간


``` java
import java.util.*;

class Solution {
    boolean[] connected; 
    public int solution(int n, int[][] computers) {
        int answer = 0;
        connected = new boolean[n];
        for(int i=0; i<n; i++) {
            if(!connected[i]) {            
                dfs(i, computers);
                answer++;
            }
        }
        return answer;
    }
    
    private void dfs(int idx, int[][] computers){
        connected[idx] = true;
        for(int i=0; i < computers[idx].length; i++){
            if(computers[idx][i] == 1 && !connected[i]) dfs(i, computers);
        }
    }
}
```
