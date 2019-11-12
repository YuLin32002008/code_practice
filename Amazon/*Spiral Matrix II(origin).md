Input: 3   
Output:   
[   
 [ 1, 2, 3 ],    
 [ 8, 9, 4 ],   
 [ 7, 6, 5 ]   
]   

   



```java
class Solution {
    public int[][] generateMatrix(int n) {
        int[][] resMatrix = new int[n][n];
        
        int rowStart = 0;
        int colStart = 0;
        int rowEnd = n-1;
        int colEnd = n-1;
        
        int k = 1;
        
        while(rowStart <= rowEnd && colStart <= colEnd){
            for(int i = colStart; i <= colEnd; i++){
                resMatrix[rowStart][i] = k;
                k++;
            }
            rowStart++;
            
            for(int i = rowStart; i <= rowEnd; i++){
                resMatrix[i][colEnd] = k;
                k++;
            }
            colEnd--;
            
            for(int i = colEnd; i >= colStart; i--){
                resMatrix[rowEnd][i] = k;
                k++;
            }
            rowEnd--;
            
            for(int i = rowEnd; i >= rowStart; i--){
                resMatrix[i][colStart] = k;
                k++;
            }
            colStart++;         
        }
        return resMatrix;        
    }
}
```
