Input: cells = [0,1,0,1,1,0,0,1], N = 7   
Output: [0,0,1,1,0,0,0,0]   
Explanation:    
The following table summarizes the state of the prison on each day:  
Day 0: [0, 1, 0, 1, 1, 0, 0, 1]  
Day 1: [0, 1, 1, 0, 0, 0, 0, 0]  
Day 2: [0, 0, 0, 0, 1, 1, 1, 0]   
Day 3: [0, 1, 1, 0, 0, 1, 0, 0]    
Day 4: [0, 0, 0, 0, 0, 1, 0, 0]   
Day 5: [0, 1, 1, 1, 0, 1, 0, 0]     
Day 6: [0, 0, 1, 0, 1, 1, 0, 0]   
Day 7: [0, 0, 1, 1, 0, 0, 0, 0]    




```java
class Solution {
        public int[] prisonAfterNDays(int[] cells, int N) {
        if(N >= 14){ // we need to loop at least 14 rounds, because after 14 steps, cells will not be the same. Therefore, this step is a must to pass test case 850:
    // Case 250 / 258 is cells = [1, 0, 0, 1, 0, 0, 0, 1], N = 826.
           for(int i = 1;i <= 14;i++){
            int[] nextCells = new int[cells.length];
                for(int j = 1;j< 7;j++){
                    if(cells[j-1] == cells[j+1]) nextCells[j] = 1;
                }
                cells = nextCells;
           } 
        }
        N = N % 14;
        for(int i = 1;i <= N;i++){
            int[] nextCells = new int[cells.length];
                for(int j = 1;j< 7;j++){
                    if(cells[j-1] == cells[j+1]) nextCells[j] = 1;
                }
                cells = nextCells;
        }
        return cells;
    }
}
```
