## ๐ ๊ฐ์ธ ํ์ด

- [ํ๋ก๊ทธ๋๋จธ์ค ํฐ์ผ๋ชฌ](https://school.programmers.co.kr/tryouts/46795/challenges)

``` java
import java.util.*;

class Solution {
    public int solution(int[] nums) {
        Set<Integer> set = new HashSet<>();
        int limit = nums.length/2;
        
        for(int num : nums){
            if(set.size() < limit) set.add(num);
            else break;
        }
        
        return set.size();
    }
}
```
