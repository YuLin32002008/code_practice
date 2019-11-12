Consider the following matrix:   
  
[   
  [1,   4,  7, 11, 15],  
  [2,   5,  8, 12, 19],    
  [3,   6,  9, 16, 22],   
  [10, 13, 14, 17, 24],   
  [18, 21, 23, 26, 30]   
]   
Given target = 5, return true.   
   
Given target = 20, return false.   


```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if(matrix.length == 0){
            return false;
        }
        
        int row = matrix.length - 1;
        int colEnd = matrix[0].length - 1;
        int col = 0;
        
        while(row >=0 && col <= colEnd ){
            if(target < matrix[row][col]){
                row--;
            }
            else if(target > matrix[row][col]){
                col++;
            }
            else if(target == matrix[row][col]){
                return true;
            }         
        }
        return false;        
    }
}

```
