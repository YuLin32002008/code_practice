Given an int array nums and an int target, find how many unique pairs in the array such that their sum is equal to target. Return the number of pairs.

## Example 1:   
Input: nums = [1, 1, 2, 45, 46, 46], target = 47   
Output: 2  
Explanation:  
1 + 46 = 47  
2 + 45 = 47   

## Example 2:
Input: nums = [1, 1], target = 2  
Output: 1  
Explanation:  
1 + 1 = 2    

## Example 3:  
Input: nums = [1, 5, 1, 5], target = 6  
Output: 1  
Explanation:  
[1, 5] and [5, 1] are considered the same.  

```java
// java O(n)
public static int getUniquePairsOpti(int[] nums, int target){
    Set<Integer> seen =  new HashSet<>();
    Map<Integer, Integer> map = new HashMap<>();
    int ans = 0;
    for (int num : nums){
        if (map.containsKey(num)){
            int key = map.get(num)*10 + num;
            if (! seen.contains(key)){
                ans++;
                seen.add(key);
            }
        } else {
            map.put(target-num, num);
        }
    }
    return ans;

}
```
