Example 1:  
Given tree s:  
  
     3  
    / \  
   4   5  
  / \  
 1   2  
Given tree t:  
   4   
  / \  
 1   2  
Return true, because t has the same structure and node values with a subtree of s.  

```java
class Solution {
    public boolean isSubtree(TreeNode s, TreeNode t) {
        return iterateTree(s,t);
    }
    
    public boolean iterateTree(TreeNode s, TreeNode t){
        return (s != null && (isSame(s,t) || iterateTree(s.left, t) || iterateTree(s.right, t)));
    }
    
    
    public boolean isSame(TreeNode s, TreeNode t){
        if(s == null && t == null){
            return true;
        }
        if(s == null || t == null){
            return false;
        }
        
        return(s.val == t.val && isSame(s.left, t.left) && isSame(s.right, t.right));
            
    }
    
}

```
