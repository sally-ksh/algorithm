
## 😃 개인 풀이

- [프로그래머스 - 숫자 문자열과 영단어](https://school.programmers.co.kr/learn/courses/30/lessons/81301)


- 처음에 입력된 문자 순서대로 하면, 순환이 복잡해져서, 숫자 문자열 기준 순환
- substring() 은 하나만 되는데, replaceAll() 처리 하지 전체 채점 통과 

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

## ✨ 다른 사람 풀이

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
