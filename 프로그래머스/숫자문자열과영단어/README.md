
## π κ°μΈ νμ΄

- [νλ‘κ·Έλλ¨Έμ€ - μ«μ λ¬Έμμ΄κ³Ό μλ¨μ΄](https://school.programmers.co.kr/learn/courses/30/lessons/81301)


- μ²μμ μλ ₯λ λ¬Έμ μμλλ‘ νλ©΄, μνμ΄ λ³΅μ‘ν΄μ Έμ, μ«μ λ¬Έμμ΄ κΈ°μ€ μν
- substring() μ νλλ§ λλλ°, replaceAll() μ²λ¦¬ νμ§ μ μ²΄ μ±μ  ν΅κ³Ό 

``` java
import java.util.*;
import java.util.stream.*;

class Solution {
    public int solution(String s) {
        Map<String, Integer> map = Map.of("zero", 0,
                                         "one", 1, 
                                          "two", 2,
                                          "three", 3,
                                          "four", 4,
                                          "five", 5,
                                          "six", 6,
                                          "seven", 7,
                                          "eight", 8,
                                          "nine", 9);
        
        for(String word : map.keySet()) {
            if(s.indexOf(word) >= 0) {
                int startIdx = s.indexOf(word);
                // s = s.substring(0, startIdx) + map.get(word) + s.substring(startIdx + word.length());
                s = s.replaceAll(word, String.valueOf(map.get(word)));
            }
        }
        return Integer.parseInt(s);
    }
}
```

## β¨ λ€λ₯Έ μ¬λ νμ΄

``` java
class Solution {
    public int solution(String s) {

        String[][] mapArr = { {"0", "zero"}, 
                              {"1", "one"}, 
                              {"2", "two"}, 
                              {"3", "three"}, 
                              {"4", "four"}, 
                              {"5", "five"}, 
                              {"6", "six"}, 
                              {"7", "seven"}, 
                              {"8", "eight"}, 
                              {"9", "nine"} };

        for(String[] map : mapArr){
            s = s.replace(map[1], map[0]);
        }

        int answer = Integer.parseInt(s);
        return answer;
    }
}
```
