
## LeetCode 56. Merge Intervals

- [56. Merge Intervals](https://leetcode.com/problems/merge-intervals/)


### π κ°μΈ νμ΄

μλ£κ΅¬μ‘°μ λν΄ μ΅κ·Όκ°λ§ λΉκ΅νλ€λ κΈ°μ€μΌλ‘ Stackμ μ¬μ© νμ΅λλ€.
λ°νμ start, end λλ€ μ λ¬ν΄μ€μΌ νλκΉ, λ£μ λ start, end λλ€ λ£μ΄μ€¬μ΅λλ€.
- stackμ΄λ queue λ₯Ό μ°λ©΄μ ν λ μ¬λ°μ΄ νλ€ λ³΄λ μΈν°λ² κ°λμ μλμλκ±° κ°μ΅λλ€.
- λ€λ₯Έ λΆμ νμ΄λ³΄λ©΄μ μΈν°λ²μ λν΄ κ³΅λΆ νμ΅λλ€.

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



### λ€λ₯Έ μ¬λ νμ΄

- λ°°μ΄ νλμ μ°Έμ‘°κ°λ§μΌλ‘ λΉκ΅νμ¬ λ³κ²½ν©λλ€.

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
