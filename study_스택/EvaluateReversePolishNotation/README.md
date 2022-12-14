
## 150. Evaluate Reverse Polish Notation

- [150. Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/)


### ๐ ๊ฐ์ธ ํ์ด
- ํ๋ผ๋ฏธํฐ๊ฐ `String[]` ์ ์ซ์๋ ์ฐ์ฐ์๊ฐ String์ผ๋ก ๋ด๊ฒจ ์์ ์ด๋ป๊ฒ ๊ตฌ๋ถํ ์ง์์ ์กฐ๊ธ ํค๋งธ์ต๋๋ค.
  - String ํ๋์ ๊ตฌ๋ถ์๋ก ๋ด๊ฒจ์ ธ ์จ๋ค๋ฉฐ split ํด์ `Character.isDigit()` ๋ฑ์ ์ฌ์ฉํ  ์ ์์ต๋๋ค. 
  - ํ์ ๋ ํ์์ ๋ฏธ๋ฆฌ ๋ด์๋๊ณ  ๊ตฌ๋ถํ๊ธฐ


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


์ฐ์ฐ์๋ฅผ ๋ด์๋ ์๋ฃ๊ตฌ์กฐ์ ์ง์คํด์ BiFunction์ ์ฌ์ฉํด ๋ดค์ต๋๋ค.
(IDE ์์ผ๋ฉด..)
- ์๋๋ ์ข ๋จ์ด์ง๋ค์.

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
