
## 150. Evaluate Reverse Polish Notation

- [150. Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/)


### 😃 개인 풀이
- 파라미터가 `String[]` 에 숫자나 연산자가 String으로 담겨 와서 어떻게 구분할지에서 조금 헤맸습니다.
  - String 하나에 구분자로 담겨져 온다며 split 해서 `Character.isDigit()` 등을 사용할 수 있습니다. 
  - 한정된 타입을 미리 담아두고 구분하기


``` java
class Solution {
    public int evalRPN(String[] tokens) {
        Set<String> operator = Set.of("+", "-", "*", "/");
        Stack<Integer> numbers = new Stack<>();
        
        for(String token : tokens){
            if (operator.contains(token)) {
                int right = numbers.pop();
                int left = numbers.pop();
                int calculated = calculate(left, token, right);
                numbers.push(calculated);
            } else {
                numbers.push(Integer.parseInt(token));
            }
        }
        return numbers.peek();
    }
    
    private int calculate(int left, String operator, int right) {
        int answer = 0;
        switch(operator){
            case "+":
                answer = left + right;
                break;
            case "-" :
                answer = left - right;
                break;
            case "*":
                answer = left * right;
                break;
            case "/" :
                answer = left / right;
                break;
        }
        return answer;
    }
}
```


연산자를 담아둔 자료구조에 집중해서 BiFunction을 사용해 봤습니다.
(IDE 없으면..)
- 속도는 좀 떨어지네요.

``` java
class Solution {
    public int evalRPN(String[] tokens) {
        Map<String, BiFunction<Integer, Integer, Integer>> calculation = new HashMap<>();
        Stack<Integer> numbers = new Stack<>();
        
        calculation.put("+", (a,b) -> a + b);
        calculation.put("-", (a,b) -> a - b);
        calculation.put("/", (a,b) -> a / b);
        calculation.put("*", (a,b) -> a * b);
        
        for(String token : tokens){
            if (calculation.containsKey(token)) {
                int right = numbers.pop();
                int left = numbers.pop();
                BiFunction<Integer, Integer, Integer> calculator = calculation.get(token);
                int calculated = calculator.apply(left, right);
                numbers.push(calculated);
            } else {
                numbers.push(Integer.parseInt(token));
            }
        }
        return numbers.peek();
    }
}
```
