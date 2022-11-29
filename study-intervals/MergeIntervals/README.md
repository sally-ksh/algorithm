
## LeetCode 56. Merge Intervals

- [56. Merge Intervals](https://leetcode.com/problems/merge-intervals/)


### 😃 개인 풀이

자료구조에 대해 최근값만 비교한다는 기준으로 Stack을 사용 했습니다.
반환시 start, end 둘다 전달해줘야 하니까, 넣을 땐 start, end 둘다 넣어줬습니다.
- stack이나 queue 를 쓰면서 풀 때 재밌어 하다 보니 인터벌 개념은 아니였던거 같습니다.
- 다른 분의 풀이보면서 인터벌에 대해 공부 했습니다.

``` java
class Solution {
    public int[][] merge(int[][] intervals) {
        Stack<Integer> stack = new Stack<>();
        
        Arrays.sort(intervals, Comparator.comparingInt(o1 -> o1[0]));
        
        for(int[] slot : intervals) {
            int start = slot[0];
            int end = slot[1];
            
            if (stack.isEmpty() || stack.peek() < start){
                stack.push(start);
                stack.push(end);

            } else if(stack.peek() >= start){
                stack.push(Math.max(stack.pop(), end));
            }            
        }
        
        int size = stack.size()/2;
        int[][] answer = new int[size][2];
        int idx = size - 1;
        while(!stack.isEmpty()){
            answer[idx][1] = stack.pop();
            answer[idx--][0] = stack.pop(); 
        }
        
        return answer;
    }
}
```



### 다른 사람 풀이

- 배열 하나의 참조값만으로 비교하여 변경합니다.

``` java
class Solution {
	public int[][] merge(int[][] intervals) {
		if (intervals.length <= 1)
			return intervals;

		// Sort by ascending starting point
		Arrays.sort(intervals, (i1, i2) -> Integer.compare(i1[0], i2[0]));

		List<int[]> result = new ArrayList<>();
		int[] newInterval = intervals[0];
		result.add(newInterval);
		for (int[] interval : intervals) {
			if (interval[0] <= newInterval[1]) // Overlapping intervals, move the end if needed
				newInterval[1] = Math.max(newInterval[1], interval[1]);
			else {                             // Disjoint intervals, add the new interval to the list
				newInterval = interval;
				result.add(newInterval);
			}
		}

		return result.toArray(new int[result.size()][]);
	}
}
```
