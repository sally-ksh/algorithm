
## π κ°μΈ νμ΄

- [νλ‘κ·Έλλ¨Έμ€ - μ κ· μμ΄λ μΆμ²](https://school.programmers.co.kr/learn/courses/30/lessons/72410)


``` java
import java.util.*;

class Solution {
    private static final char PERIOD = '.';
    public String solution(String new_id) {
        String regex = "[^-_.0-9a-z]";
        String lowerCase = new_id.toLowerCase();
        String text = lowerCase.replaceAll(regex, "");
        
        StringBuilder sb = new StringBuilder();
        int start = 0;
        int length = text.length();
        sb.append(text.charAt(start));
        for(int end=1; end<length; end++){
            while(end < length && text.charAt(start) == PERIOD && text.charAt(end) == PERIOD) {
                end++;
            }
            if (end >= length){
                break;
            }
            sb.append(text.charAt(end));
            start = end;
        }

        if (sb.charAt(0) == PERIOD) {
            sb.deleteCharAt(0);
        }
        
        removeLastIdx(sb);
        
        if (isBlanked(sb)) {
			sb.append("a");
		}

        if (sb.length() > 15){
            sb.delete(15, sb.length());
            removeLastIdx(sb);
        }
        
        while(sb.length() < 3) {
            sb.append(sb.charAt(getLastIdx(sb)));
        }
        
        return sb.toString();
    }
    
    private void removeLastIdx(StringBuilder sb){
        if (isBlanked(sb)) {
			return;
		}
        if (sb.charAt(getLastIdx(sb)) == PERIOD){
            sb.deleteCharAt(getLastIdx(sb));
        }
    }
    
    private int getLastIdx(StringBuilder sb){
        return sb.length() - 1;
    }
    
    private boolean isBlanked(StringBuilder sb) {
		return  (Objects.isNull(sb) || sb.length() == 0);
	}
}
```


## β¨ λ€λ₯Έ μ¬λ νμ΄

- μ κ·μ : 1κ° μ΄μ μ°μλ λ§μΉ¨ν μ κ±°
    ``` java
    temp = temp.replaceAll("[.]{2,}",".");
    ```

- μ κ·μ : μ/λ€ λ§μΉ¨ν 1κ°λ§ μ κ±°
    ``` java
    temp = temp.replaceAll("^[.]|[.]$","");
    ```


``` java
class Solution {
    public String solution(String new_id) {
        String answer = "";
        String temp = new_id.toLowerCase();

        temp = temp.replaceAll("[^-_.a-z0-9]","");
        System.out.println(temp);
        temp = temp.replaceAll("[.]{2,}",".");
        temp = temp.replaceAll("^[.]|[.]$","");
        System.out.println(temp.length());
        if(temp.equals(""))
            temp+="a";
        if(temp.length() >=16){
            temp = temp.substring(0,15);
            temp=temp.replaceAll("^[.]|[.]$","");
        }
        if(temp.length()<=2)
            while(temp.length()<3)
                temp+=temp.charAt(temp.length()-1);

        answer=temp;
        return answer;
    }
}
```
