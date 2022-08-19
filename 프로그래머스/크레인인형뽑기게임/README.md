
## 😃 개인 풀이

- [프로그래머스 - 신규 아이디 추천](https://school.programmers.co.kr/learn/courses/30/lessons/72410)


``` java
import java.util.*;
import java.util.stream.*;

class Solution {
    public int solution(int[][] board, int[] moves) {
        int answer = 0;
        int size = board.length;
        Map<Integer, Queue<Integer>> map = IntStream.rangeClosed(1, size)
            .boxed()
            .collect(Collectors.toMap(idx -> idx, idx -> new LinkedList<Integer>()));
        
        for(int[] row : board){
            for(int i=0; i < size; i++){
                int cell = row[i];
                if( cell!= 0){
                    map.get(i+1).offer(cell);
                }
            }
        }
        
        Stack<Integer> stack = new Stack<>();
        for(int move : moves){
            if(!map.get(move).isEmpty()){
                if (!stack.isEmpty() && stack.peek() == map.get(move).peek()){
                    answer+=2;
                    map.get(move).poll();
                    stack.pop();
                    continue;
                }
                stack.push(map.get(move).poll());
            }
        }
        return answer;
    }
}
```

## ✨ 다른 사람 풀이

``` java
import java.util.Stack;
class Solution {
    static Stack<Integer> stack = new Stack<>();
    static int answer = 0;

    public int solution(int[][] board, int[] moves) {
        for(int idx : moves) {
            board = pick(board, idx - 1);
        }
        return answer;
    }
    static int[][] pick(int[][] board, int idx) {
        for(int i = 0 ; i < board.length ; i++) {
            if(board[i][idx] == 0) continue;

            if(!stack.isEmpty() && stack.peek() == board[i][idx]) {
                answer += 2;
                stack.pop();
                board[i][idx] = 0;
                break;
            }
            stack.push(board[i][idx]);
            board[i][idx] = 0;
            break;
        }
        return board;
    }
}
```
