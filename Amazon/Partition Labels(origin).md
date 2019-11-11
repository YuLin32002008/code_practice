Input: S = "ababcbacadefegdehijhklij"  
Output: [9,7,8]  
Explanation:  
The partition is "ababcbaca", "defegde", "hijhklij".  
This is a partition so that each letter appears in at most one part.  
A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits S into less parts.  



```java
class Solution {
    public List<Integer> partitionLabels(String S) {
        int[] last = new int[26];
        
        for(int i = 0; i < S.length(); i++){
        	last[S.charAt(i) - 'a'] = i;
        }
        
        List<Integer> res = new ArrayList<>();
        
        int j = 0;
        int start = 0;
        
        for(int i = 0; i<S.length(); i++){
        	j = Math.max(j, last[S.charAt(i) - 'a']);
        	if(i == j){
        		res.add(j - start + 1);
        		start = j+1;
        	}
        }
        return res;        
        
    }
}
```
