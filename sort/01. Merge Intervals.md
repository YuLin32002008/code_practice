Given a collection of intervals, merge all overlapping intervals.

## Example 1:
Input: [[1,3],[2,6],[8,10],[15,18]]  
Output: [[1,6],[8,10],[15,18]]  
Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].  

## Example 2:
Input: [[1,4],[4,5]]   
Output: [[1,5]]   
Explanation: Intervals [1,4] and [4,5] are considered overlapping.   

NOTE: input types have been changed on April 15, 2019. Please reset to default code definition to get new method signature.  



## My solution1: Sort
```java
    public int[][] merge(int[][] intervals) {
        if(intervals.length == 0 || intervals.length == 1){
    		return intervals;
    	}
    	
    	
    	List<int[]> res = new ArrayList<>();
    	Arrays.sort(intervals , 
    			(a, b) -> a[0] - b[0]);
    	res.add(intervals[0]);
    	int j = 0;
    	for(int i = 1; i<intervals.length; i++){
    		if(intervals[i][0] > res.get(j)[1]){
    			res.add(intervals[i]);
                j++;
    		}
    		else if(intervals[i][0] <= res.get(j)[1] && intervals[i][1] > res.get(j)[1]){
    			res.get(j)[1] = intervals[i][1];
    		}	
    	}	
        return res.toArray(new int[res.size()][]); 
    }
```



