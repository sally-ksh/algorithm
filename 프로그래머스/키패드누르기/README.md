
## 😃 개인 풀이

- [프로그래머스 - 키패드 누르기](https://school.programmers.co.kr/learn/courses/30/lessons/67256)

### JAVA

- Map.of() : 10개의 값까지만 초기화 가능
  - 채점 결과 2개 실패 : 시작위치에서의 값 필요 한 듯하여
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

- java Map 초기화 2가지 중
  - put();
    - Map.of() 에서 수정하면서 `put & ;`  등 일일이 수정
  - Map.ofEntries()
    - 불변 객체
    - Map.entry() 로...
  - stream 이용
    - 외우기 번거로우나, Object 배열안에 넣어서 나중에 타입캐스팅만 해주면서 `put & ;` 보다는 나아보임 😑
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

#### 답안

- 메서드 분리하다 보니 파라미터 줄이고자 전역변수 처리가 늘었다.

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
                // 2,5,0,8 - 가까운순, 동일 : hand
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

## ✨ 다른 사람 풀이

- switch-case 로 좀더 빠른 처리
- 번호판 계산 방식 응용 등 [블로그](https://shrimp-burger.tistory.com/185)

> 번호 간 거리 = ((현재 번호 - 다음 번호) / 3) + ((현재 번호 - 다음 번호) % 3)

