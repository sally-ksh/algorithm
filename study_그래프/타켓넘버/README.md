
### [νμΌλλ²](https://school.programmers.co.kr/learn/courses/30/lessons/43165)

## π κ°μΈ νμ΄

- μλ£κ΅¬μ‘° : κ·Έλν
- μκ° λ³΅μ‘λ : O(2^n), κ³΅κ°λ³΅μ‘λ : O(1)

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
