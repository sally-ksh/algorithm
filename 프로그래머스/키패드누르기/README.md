
## π κ°μΈ νμ΄

- [νλ‘κ·Έλλ¨Έμ€ - ν€ν¨λ λλ₯΄κΈ°](https://school.programmers.co.kr/learn/courses/30/lessons/67256)

### JAVA

- Map.of() : 10κ°μ κ°κΉμ§λ§ μ΄κΈ°ν κ°λ₯
  - μ±μ  κ²°κ³Ό 2κ° μ€ν¨ : μμμμΉμμμ κ° νμ ν λ―νμ¬
    ``` java
       private static final Map<Integer, Point> coordinates = Map.of(0, Point.of(3,1),
                                                                     1, Point.of(0,0),
                                                                     2, Point.of(0,1),
                                                                     3, Point.of(0,2),
                                                                     4, Point.of(1,0),
                                                                     5, Point.of(1,1),
                                                                     6, Point.of(1,2),
                                                                     7, Point.of(2,0),
                                                                     8, Point.of(2,1),
                                                                     9, Point.of(2,2));
    ```

- java Map μ΄κΈ°ν 2κ°μ§ μ€
  - put();
    - Map.of() μμ μμ νλ©΄μ `put & ;`  λ± μΌμΌμ΄ μμ 
  - Map.ofEntries()
    - λΆλ³ κ°μ²΄
    - Map.entry() λ‘...
  - stream μ΄μ©
    - μΈμ°κΈ° λ²κ±°λ‘μ°λ, Object λ°°μ΄μμ λ£μ΄μ λμ€μ νμμΊμ€νλ§ ν΄μ£Όλ©΄μ `put & ;` λ³΄λ€λ λμλ³΄μ π
    ``` java
        private static final Map<Integer, Point> coordinates = new HashMap<>(){{
                                                                    put(0, Point.of(3,1));
                                                                    put(10, Point.of(3,0));
                                                                    put(12, Point.of(3,2));
                                                                    put(1, Point.of(0,0));
                                                                    put(2, Point.of(0,1));
                                                                    put(3, Point.of(0,2));
                                                                    put(4, Point.of(1,0));
                                                                    put(5, Point.of(1,1));
                                                                    put(6, Point.of(1,2));
                                                                    put(7, Point.of(2,0));
                                                                    put(8, Point.of(2,1));
                                                                    put(9, Point.of(2,2));
        }};
    ```

#### λ΅μ

- λ©μλ λΆλ¦¬νλ€ λ³΄λ νλΌλ―Έν° μ€μ΄κ³ μ μ μ­λ³μ μ²λ¦¬κ° λμλ€.

    ``` java
    import java.util.*;
    import java.util.stream.*;
    
    class Point {
        private int y;
        private int x;
        
        public static Point of(int y, int x){
            Point p = new Point();
            p.y = y;
            p.x = x;
            return p;
        }
        
        public int getY(){
            return this.y;
        }
        
        public int getX(){
            return this.x;
        }
    }
    
    class Solution {
        private static final String L = "L";
        private static final String R = "R";
        private static final Map<Integer, String> map = Map.of(1,L, 4,L, 7,L,
                                             3,R, 6,R, 9,R);
        
        private static final Map<Integer, Point> coordinates = Stream.of(new Object[][] {
            {0, Point.of(3,1)},
            {10, Point.of(3,0)},
            {12, Point.of(3,2)},
            {1, Point.of(0,0)},
            {2, Point.of(0,1)},
            {3, Point.of(0,2)},
            {4, Point.of(1,0)},
            {5, Point.of(1,1)},
            {6, Point.of(1,2)},
            {7, Point.of(2,0)},
            {8, Point.of(2,1)},
            {9, Point.of(2,2)},
        }).collect(Collectors.toMap(data -> (int) data[0], data ->(Point) data[1]));
        
        private static int l = 10;
        private static int r = 12;
        
        public String solution(int[] numbers, String hand) {
            Map<String, String> priority = Map.of("right", R, "left", L);
            StringBuilder sb = new StringBuilder();
            
            for(int number : numbers){
                if (map.containsKey(number)) {
                    sb.append(map.get(number));
                    move(number);
                    continue;
                }
                // 2,5,0,8 - κ°κΉμ΄μ, λμΌ : hand
                Point lp = coordinates.get(l);
                Point rp = coordinates.get(r);
                Point next = coordinates.get(number);
                
                int ld = Math.abs(lp.getY() - next.getY()) + Math.abs(lp.getX() - next.getX());
                int rd = Math.abs(rp.getY() - next.getY()) + Math.abs(rp.getX() - next.getX());
                if(ld == rd) {
                    moveByDirction(priority.get(hand), sb, number);
                } else if(ld < rd) {
                    moveByDirction(L, sb, number);
                } else {
                    moveByDirction(R, sb, number);
                }
            }
            return sb.toString();
        }
        
        private void move(int number){
            if (map.get(number).equals(L)){
                l = number;
            } else {
                r = number;
            }
        }
        
        private void moveByDirction(String direction, StringBuilder sb, int nextPoint){
            if(direction.equals(L)) {
                sb.append(L);
                l = nextPoint;
            } else {
                sb.append(R);
                r = nextPoint;
            }
        }
    }
    ```

## β¨ λ€λ₯Έ μ¬λ νμ΄

- switch-case λ‘ μ’λ λΉ λ₯Έ μ²λ¦¬
- λ²νΈν κ³μ° λ°©μ μμ© λ± [λΈλ‘κ·Έ](https://shrimp-burger.tistory.com/185)

> λ²νΈ κ° κ±°λ¦¬ = ((νμ¬ λ²νΈ - λ€μ λ²νΈ) / 3) + ((νμ¬ λ²νΈ - λ€μ λ²νΈ) % 3)

