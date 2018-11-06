# Two Sum
Given an array of integers, return indices of the two numbers such that they add up to a specific target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.

Given nums = [2, 7, 11, 15], target = 9,
Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].

# My Solution(Wrong)
```java
public class Solution {
	 public static int[] twoSum(int[] nums, int target) {
		 	int[] res = {0,0};
	        for(int i=0;i<nums.length;i++){
	        	for(int j=1;j<nums.length;j++){
	        		if(target==nums[i]+nums[j]){
	        			res[0]=i;
	        			res[1]=j;
	        			break;
	        		}
	        	}
	        }
			return res;
	    }
}
```
