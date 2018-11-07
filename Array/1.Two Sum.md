# Two Sum
Given an array of integers, return indices of the two numbers such that they add up to a specific target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.

Given nums = [2, 7, 11, 15], target = 9,
Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].

* 1. Brute Force 
```java
//My Solution (Wrong)
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

// After evaluate.
public class Solution {
	 public static int[] twoSum(int[] nums, int target) {
	        for(int i=0;i<nums.length;i++){
	        	for(int j=1;j<nums.length;j++){
	        		if(target==nums[i]+nums[j]){

	        			return new int[]{i,j};
	        		}
	        	}
	        }
	        throw new IllegalArgumentException("No two sum solution");
	    }

```
It is a Brute Force algorithm. 
Time complexity: O(n^2)
Space complexity: O(1)

* 2. Two-pass Hash table
**What is the best way to maintain a mapping of each element in the array to its index? A hash table.**
```java
public static int[] twoSum(int[] nums, int target) {
		 	Map<Integer, Integer> map = new HashMap<> ();
	        for(int i=0;i<nums.length;i++){
	        	map.put(nums[i],i);
	        	}
	        
	        for(int i=0;i<nums.length;i++){
	        	int complement = target-nums[i];
	        	if(map.containsValue(complement)&& map.get(complement)!=i){
	        		return new int[] {i,map.get(complement)};
	        	}
	        }
	        
	        throw new IllegalArgumentException("No two sum solution");
	        }
```
Time complexity: O(n)
Space complexity: O(n)

* 3. One-pass Hash table
While we iterate and inserting elements into the table, we also look back to check if current element's complement already exists in the table. If it exists, we have found a solution and return immediately.
```java
	 public static int[] twoSum(int[] nums, int target) {
		 	Map<Integer, Integer> map = new HashMap<> ();
	        for(int i=0;i<nums.length;i++){     	
	        	int complement = target-nums[i];
	        	if(map.containsKey(complement)){
	        		return new int[] {i,map.get(complement)};
	        		}
	        	map.put(nums[i],i);
	        	} 
	        throw new IllegalArgumentException("No two sum solution");
	        }
```
Time complexity: O(n)
Space complexity: O(n)
