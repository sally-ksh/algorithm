
## LeetCode 253. Meeting Rooms II

- [253. Meeting Rooms II](https://leetcode.com/problems/meeting-rooms-ii/)


### π κ°μΈ νμ΄

μ²μμ start time κΈ°μ€μΌλ‘ μ λ ¬ ν νμ€νΈ νλ,

[2,11],[6,16],[11,16] μμ μΌ λ, `[2,11] β [11,16]` λ‘ νλμ νμμ€λ‘ μ¬νμ© ν  μ μκ² ν΄μΌ νμ΅λλ€.

- start time κΈ°μ€ μ λ ¬ νμ
- end time κΈ°μ€ μ λ ¬ νμ

λμ νλμ μ λ ¬λ‘ νλ κ±΄ μ΄λ €μ μ£  γγ

λΆλ¦¬ ν΄μ μκ°νκ³ μ νλ, μμ μκ° λλ‘ μ λ ¬νμ¬ μννλ©΄μ, μννλ μ’λ£ μκ°κ³Ό νμ¬ νμμ€μ μ’λ£μκ° κ°μ₯ μμ κ°κ³Ό λΉκ΅νλ©΄μ, κ°μ₯ μμ κ°μ΄ ν΄κ²°λ  λ λ€μμ μμ μ’λ£μκ° κ°μ§ κ°μ μλ €μ£Όλ μλ£κ΅¬μ‘°λ₯Ό ν΅ν΄ ν΄κ²°λμ§ μμ νμμ€λ€μ νμν νμμ€λ‘ λ°ννκ³ μ νμ΅λλ€.

- μ’μ μλ£κ΅¬μ‘°λ PriorityQueue


``` java
	class Solution {
            public int minMeetingRooms(int[][] intervals) {
                Arrays.sort(intervals, (a,b) -> a[0] - b[0]);
                PriorityQueue<Integer> rooms = new PriorityQueue<>();
                
                rooms.offer(intervals[0][1]);
                
                for(int i=1; i<intervals.length; i++){
                    if (intervals[i][0] >= rooms.peek()) {
                        rooms.poll();
                    }
                    rooms.offer(intervals[i][1]);
                }
                
                return rooms.size();
            }
        }
```

- μκ° λ³΅μ‘λ O(N log N)
  - min-Heap μλ£κ΅¬μ‘°μμ μΆμΆμλ§λ€ logN μκ°λ³΅μ‘λλ‘ μ΅μμ κ²½μ° Nλ² λ°λ³΅
- κ³΅κ° λ³΅μ‘λ (N)
  - min-Heap μλ£κ΅¬μ‘°μ μ΅μμ κ²½μ° Nκ° λͺ¨λ λ€μ΄κ° μ μλ€


### π λ€λ₯Έ νμ΄

- start time κΈ°μ€ μ λ ¬ νμ
- end time κΈ°μ€ μ λ ¬ νμ

μμ 2κ°μ§ μ‘°κ±΄μΌλ‘ κ³ λ―Όνμλλ°μ.
μ€μ  λΆλ¦¬ν΄μ μκ°ν΄ λ΄λ λμμ΅λλ€. (μμΈν λ΄μ©μ LeetCode νμ΄μ μ°Έκ³ ν΄ μ£ΌμΈμ. μ½λλ νμ΄ μ λ¦¬ ν μ κ° κ΅¬ν ν΄μ λ€λ₯Ό μ μμ΅λλ€.)

- ν¬μΈνΈ : νμ μ’λ£μκ°μ μ΄μ©κ°λ₯ν νμμ€μ κ΅¬ν  μ μλμ§κ° μ€μνλ€.
- μμκ³Ό μ’λ£μκ°μ κ°κ° λΆλ¦¬ν΄μ μ λ ¬λ μνλ‘ λ΄λλ€.
    - μ°κ²° λ  νμκ° μλκ² ν¬μΈνΈ
- κ°κ°μ indexλ₯Ό start pointer, end pointer λ‘ λλ©΄
    - κ°κ°μ κ°λ€μ μ κ·Όνμ¬ λΉκ΅νλ€.
    - start pointer β₯ end pointer μ΄λ©΄ νμμ€μ μ¬μ¬μ©ν  μ μλ€.
        - end pointer λ₯Ό μ¦κ°μν¨λ€.
- start pointer < end pointer νμλ μμν΄μΌ νλκΉ, μ¦ λ€λ₯Έ νμμ€μ ν λΉν΄μΌ νλ€.
    - start pointer λ₯Ό μ¦κ°μν¨λ€.


``` java
class Solution {
    public int minMeetingRooms(int[][] intervals) {
        List<Integer> starts = new ArrayList<>();
        List<Integer> ends = new ArrayList<>();

        Arrays.stream(intervals)
            .forEach(
                interval -> {
                    starts.add(interval[0]);
                    ends.add(interval[1]);
            });
        Collections.sort(starts);
        Collections.sort(ends);
        
        int sIdx = 0, eIdx = 0, length = intervals.length;
        int roomCount = 0;
        while(sIdx < length){
            if(starts.get(sIdx) >= ends.get(eIdx)) {
                roomCount--;
                eIdx++;
            } 
            roomCount++;
            sIdx++;
        }
        return roomCount;
    }
}
```

- μκ°λ³΅μ‘λ O(NlogN)
  - μμμκ°κ³Ό μ’λ£μκ°μ κ°κ°μ List λ€ μ λ ¬μμ NlogN
  - sIdx κ° N λ² μν
- κ³΅κ°λ³΅μ‘λ O(N)
  - μμμκ°κ³Ό μ’λ£μκ°μ κ°κ°μ List λ€
