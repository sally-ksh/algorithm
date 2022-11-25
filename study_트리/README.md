## LeetCode 104. Maximum Depth of Binary Tree

- [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)


### 😃 개인 풀이


- depth를 전역변수로 쓰는 방식이 마음에 걸렸는데, 종료조건에서 반환 값을 급하게 생각못하다 보니 전역 변수 두고 작성하게 됐었습니다. 
``` java
class Solution {
    int depth = 0;
    
    public int maxDepth(TreeNode root) {
        if(Objects.isNull(root)) {
            return depth;
        }
        
        depth++;
        int leftLevel = maxDepth(root.left);
        int rightLevel = maxDepth(root.right);
        depth--;
        return Math.max(leftLevel, rightLevel);
    }
}
```



- BFS 방식으로는 각 레벨별로 Queue의 사이즈를 통해 순회 합니다.

``` java
class Solution {
    public int maxDepth(TreeNode root) {
        if(Objects.isNull(root)) {
            return 0;
        }
        
        Queue<TreeNode> q = new LinkedList<>();
        q.offer(root);
        int depth = 0;
        
        while(!q.isEmpty()) {
            int size = q.size();
            depth++;
            
            for(int i=0; i<size; i++){
                TreeNode node = q.poll();
                if(node.left != null) q.offer(node.left);
                if(node.right != null) q.offer(node.right);
            }
        }
        return depth;
    }
}
```



- DFS 의 stack 이용한 구현


``` java
class Solution {
    class Level {
        private TreeNode node;
        private int depth;
        
        public Level(TreeNode node, int depth){
            this.node = node;
            this.depth = depth;
        }
        
        public int nextLevel(){
            return depth+1;
        }
        
        public boolean notEmptyNode(){
            return !Objects.isNull(this.node);
        }
        
        public TreeNode left(){
            return node.left;
        }
        
        public TreeNode right(){
            return node.right;
        }
    }
    public int maxDepth(TreeNode root) {
        Stack<Level> stack = new Stack();
        
        stack.push(new Level(root, 1));
        int maxLevel = 0;
        
        while(!stack.isEmpty()){
            Level cur = stack.pop();
            if(cur.notEmptyNode()) {
                maxLevel = Math.max(maxLevel, cur.depth);
                stack.push(new Level(cur.left(), cur.nextLevel()));
                stack.push(new Level(cur.right(), cur.nextLevel()));
            }
        }
        return maxLevel;
    }
}
```
- `int maxLevel = 0;` 들어온 root 가 null일 경우 반환을 0으로해주기 위해 초기화는 zero
- `if(cur.notEmptyNode())` 각 left, right 별로 empty 체크 대신
    - null 로 들어갔다면 다음 pop 결과 Level의 node 는 null 이어서 진행 안하게 하기 위해서


---

### 👍 다른 사람 풀이 참조

- DFS 니까, 가장 아래까지 가서 올라오면서 각각 depth 별로 1씩 더해서 루크까지 온다고 생각하면 null 일 때 0을 반환해주면 됩니다.

``` java
class Solution {
    public int maxDepth(TreeNode root) {
        if(Objects.isNull(root)) {
            return 0;
        }
        
        return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
    }
}
```
