
## LeetCode 253. Meeting Rooms II

- [253. Meeting Rooms II](https://leetcode.com/problems/meeting-rooms-ii/)


### 😃 개인 풀이

처음에 start time 기준으로 정렬 후 테스트 하니,

[2,11],[6,16],[11,16] 순서 일 때, `[2,11] → [11,16]` 로 하나의 회의실로 재활용 할 수 있게 해야 했습니다.

- start time 기준 정렬 필요
- end time 기준 정렬 필요

둘을 하나의 정렬로 하는 건 어려웠죠 ㅎㅎ

분리 해서 생각하고자 하니, 시작 시간 대로 정렬하여 순회하면서, 순회하는 종료 시간과 현재 회의실의 종료시간 가장 작은 값과 비교하면서, 가장 작은 값이 해결될 때 다음의 작은 종료시간 가진 값을 알려주는 자료구조를 통해 해결되지 않은 회의실들을 필요한 회의실로 반환하고자 했습니다.

- 좋은 자료구조는 PriorityQueue


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

- 시간 복잡도 O(N log N)
  - min-Heap 자료구조에서 추출시마다 logN 시간복잡도로 최악의 경우 N번 반복
- 공간 복잡도 (N)
  - min-Heap 자료구조에 최악의 경우 N개 모두 들어갈 수 있다


### 👍 다른 풀이

- start time 기준 정렬 필요
- end time 기준 정렬 필요

위의 2가지 조건으로 고민했었는데요.
실제 분리해서 생각해 봐도 됐었습니다. (자세한 내용은 LeetCode 풀이을 참고해 주세요. 코드는 풀이 정리 후 제가 구현 해서 다를 수 있습니다.)

- 포인트 : 회의 종료시간에 이용가능한 회의실을 구할 수 있는지가 중요하다.
- 시작과 종료시간을 각각 분리해서 정렬된 상태로 담는다.
    - 연결 될 필요가 없는게 포인트
- 각각의 index를 start pointer, end pointer 로 두면
    - 각각의 값들에 접근하여 비교한다.
    - start pointer ≥ end pointer 이면 회의실을 재사용할 수 있다.
        - end pointer 를 증가시킨다.
- start pointer < end pointer 회의는 시작해야 하니까, 즉 다른 회의실을 할당해야 한다.
    - start pointer 를 증가시킨다.


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

- 시간복잡도 O(NlogN)
  - 시작시간과 종료시간의 각각의 List 들 정렬에서 NlogN
  - sIdx 가 N 번 순회
- 공간복잡도 O(N)
  - 시작시간과 종료시간의 각각의 List 들
