## LeetCode 104. Maximum Depth of Binary Tree

- [104. Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)


### π κ°μΈ νμ΄


- depthλ₯Ό μ μ­λ³μλ‘ μ°λ λ°©μμ΄ λ§μμ κ±Έλ Έλλ°, μ’λ£μ‘°κ±΄μμ λ°ν κ°μ κΈνκ² μκ°λͺ»νλ€ λ³΄λ μ μ­ λ³μ λκ³  μμ±νκ² λμμ΅λλ€. 
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



- BFS λ°©μμΌλ‘λ κ° λ λ²¨λ³λ‘ Queueμ μ¬μ΄μ¦λ₯Ό ν΅ν΄ μν ν©λλ€.

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



- DFS μ stack μ΄μ©ν κ΅¬ν


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
- `int maxLevel = 0;` λ€μ΄μ¨ root κ° nullμΌ κ²½μ° λ°νμ 0μΌλ‘ν΄μ£ΌκΈ° μν΄ μ΄κΈ°νλ zero
- `if(cur.notEmptyNode())` κ° left, right λ³λ‘ empty μ²΄ν¬ λμ 
    - null λ‘ λ€μ΄κ°λ€λ©΄ λ€μ pop κ²°κ³Ό Levelμ node λ null μ΄μ΄μ μ§ν μνκ² νκΈ° μν΄μ


---

### π λ€λ₯Έ μ¬λ νμ΄ μ°Έμ‘°

- DFS λκΉ, κ°μ₯ μλκΉμ§ κ°μ μ¬λΌμ€λ©΄μ κ°κ° depth λ³λ‘ 1μ© λν΄μ λ£¨ν¬κΉμ§ μ¨λ€κ³  μκ°νλ©΄ null μΌ λ 0μ λ°νν΄μ£Όλ©΄ λ©λλ€.

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
