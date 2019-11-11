Input:   
[['S', 'O', 'O', 'S', 'S'],   
 ['D', 'O', 'D', 'O', 'D'],   
 ['O', 'O', 'O', 'O', 'X'],   
 ['X', 'D', 'D', 'O', 'O'],   
 ['X', 'D', 'D', 'D', 'O']]   
   
Output: 3   
Explanation:   
You can start from (0,0), (0, 3) or (0, 4). The treasure locations are (2, 4) (3, 0) and (4, 0). Here the shortest route is (0, 3), (1, 3), (2, 3), (2, 4).



## 1. BFS
```java
// https://leetcode.com/discuss/interview-question/356150
public class Main {
    private static final int[][] DIRS = {{0, 1}, {1, 0}, {-1, 0}, {0, -1}};

    public static int minDist(char[][] grid) {
        Queue<Point> q = collectSources(grid);
        for (int dist = 0; !q.isEmpty(); dist++) {
            for (int sz = q.size(); sz > 0; sz--) {
                Point p = q.poll();
                
                if (grid[p.r][p.c] == 'X') return dist;
                grid[p.r][p.c] = 'D'; // mark as visited
                
                for (int[] dir : DIRS) {
                    int r = p.r + dir[0];
                    int c = p.c + dir[1];
                    if (isSafe(grid, r, c)) {
                        q.add(new Point(r, c));
                    }
                }
                
            }
        }
        return -1;
    }
    
    private static Queue<Point> collectSources(char[][] grid) {
        Queue<Point> sources = new ArrayDeque<>();
        for (int r = 0; r < grid.length; r++) {
            for (int c = 0; c < grid[0].length; c++) {
                if (grid[r][c] == 'S') {
                    sources.add(new Point(r, c));
                }
            }
        }
        return sources;
    }
    
    private static boolean isSafe(char[][] grid, int r, int c) {
        return r >= 0 && r < grid.length && c >= 0 && c < grid[0].length && grid[r][c] != 'D';
    }
    
    private static class Point {
        int r, c;
        Point(int r, int c) {
            this.r = r;
            this.c = c;
        }
    }

    public static void main(String[] args) {        
        char[][] grid = {
            {'S', 'O', 'O', 'S', 'S'},
            {'D', 'O', 'D', 'O', 'D'},
            {'O', 'O', 'O', 'O', 'X'},
            {'X', 'D', 'D', 'O', 'O'},
            {'X', 'D', 'D', 'D', 'O'}}; 
        test(minDist(grid), 3);
    }
    
    private static void test(int actual, int expected) {
        if (actual == expected) {
            System.out.println("PASSED!");
        } else {
            System.out.println(String.format("FAILED! Expected: %d, but got: %d", expected, actual));
        }
    }
}
```

## 2. DP

```java
// "static void main" must be defined in a public class.
public class Main {
    static int m, n;
    public static void main(String[] args) {
        char[][] input = new char[][]{{'S', 'O', 'O', 'S', 'S'},
                                      {'D', 'O', 'D', 'O', 'D'},
                                      {'O', 'O', 'O', 'O', 'X'},
                                      {'X', 'D', 'D', 'O', 'O'},
                                      {'X', 'D', 'D', 'D', 'O'}};
        int rst = multiSourceShortest(input);
        System.out.println(rst);
    }
    
    public static int multiSourceShortest(char[][] matrix) {
        int n = matrix.length;
        int m = matrix[0].length;
        int MAX = m*n;
        int[][] rst = new int[n][m];
        int path = Integer.MAX_VALUE;

        // Sweep from upper left to bottom right
        for(int i = 0; i < n; i++){
            for(int j = 0; j < m; j++){
                if(matrix[i][j] == 'D'){
                    rst[i][j] = MAX;
                } else if(matrix[i][j] == 'X'){
                    rst[i][j] = 0;
                } else {
                    int cellAbove = i > 0 ? rst[i-1][j] : MAX;
                    int cellLeft = j > 0 ? rst[i][j-1] : MAX;
                    rst[i][j] = Math.min(cellAbove, cellLeft) + 1;
                }
            }
        }
        
        // Sweep from bottom right to upper left
        for(int i = n-1; i >= 0; i--){
            for(int j = m-1; j >= 0; j--){
                if(matrix[i][j] != 'D'){
                    int cellBelow = i < n-1 ? rst[i+1][j] : MAX;
                    int cellRight = j < m-1 ? rst[i][j+1] : MAX;
                    rst[i][j] = Math.min(rst[i][j], Math.min(cellBelow, cellRight) + 1);
                }
                
                // pick out the source nodes and get min path length
                if(matrix[i][j] == 'S'){
                    path = Math.min(path, rst[i][j]);
                }
            }
        }
        
        return path;   
    }
}
```
