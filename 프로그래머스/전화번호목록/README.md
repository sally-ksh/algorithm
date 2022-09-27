
#### [프로그래머스 전화번호목록](https://school.programmers.co.kr/learn/courses/30/lessons/42577)


## 😃 개인 풀이

- 해시 문제라고들 하는데 유난히, 해시로 접근되지 않았었다.
- 트라이로 풀어보면서, 테스트 케이스 몇개를 통과하지 못 했고, 중간의 조건문으로 인해, 정렬이 필요했었다.
- 시간복잡도 : O( n log n + n * m) , 공간복잡도 O(n)

``` java
import java.util.*;

class Node {
    Character key;
    boolean isEnd;
    HashMap<Character, Node> children;
    
    Node(Character kye){
        this.key = kye;
        this.isEnd = false;
        this.children = new HashMap<>();
    }
}

class Solution {
    public boolean solution(String[] phone_book) {
        boolean answer = true;
        
        Node root = new Node(' ');
        for (String phoneNumber : phone_book) {
            Node current = root;
            for (Character number : phoneNumber.toCharArray()){
                if(current.children.get(number) == null){
                    current.children.put(number, new Node(number));
                }
                current = current.children.get(number);
                if (current.isEnd){
                    return false;
                }
            }
            current.isEnd = true;
        }
        
        return true;
    }
}
```

### 👍 해시 시간 복잡도 : O(n*m), 공간복잡도 O(n)

- 1 차원 배열 -> Set : `Set.of()`
- 

``` java
import java.util.*;

class Solution {
    public boolean solution(String[] phoneBook) {
        Set<String> phoneNumbers = Set.of(phoneBook);
        
        for(String phone : phoneBook){
            for(int i = 1; i<phone.length(); i++){
                String prefix = phone.substring(0, i);
                if (phoneNumbers.contains(prefix)){
                    return false;
                }
            }
        }
        return true;
    }
}
```


### 다른 사람 풀이

- startsWith()의 시간 복잡도가 O(n) [ref](https://helloacm.com/string-startswith-implementation-in-java/#:~:text=The%20time%20complexity%20is%20O,number%20of%20characters%20in%20prefix.)
  - indexOf() 보다 좋다고 하는데, 효율성 테스트 케이스에서 좀더 좋게 나왔고, 그외에는 indexOf() 가 더 좋게 나온 경우가 많았다.
  - 한 글자 비교는 charAt()이 더 좋다고도 한다.
- for문의 시간 복잡도는 O( nlogn + n * m), 공간 X
- Arrays.sort()의 시간 복잡도는 O(n log n)

``` java
class Solution {
    public boolean solution(String[] phone_book) {
        Arrays.sort(phone_book);

        for(int i=0; i<phone_book.length-1;i++){
            if(phone_book[i+1].startsWith(phone_book[i])){
                return false;
            }
        }

        return true;
    }
}
```
