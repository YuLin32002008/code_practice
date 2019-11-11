
## Example:
Input:  
numRouters = 7  
numLinks = 7  
Links = [[0,1], [0, 2], [1, 3], [2, 3], [2, 5], [5, 6], [3,4]]  
  
Output:  
[2, 3, 5]  

```java
package Amazon;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashMap;
import java.util.HashSet;
import java.util.List;
import java.util.Map;
import java.util.Set;

public class CriticalRouters {
	static int time = 0;

	public static void main(String[] args) {
		int numRouters1 = 5;
		int numLinks1 = 6;
		int[][] links1 = {{0, 1}, {1, 2}, {0, 2}, {2, 3}, {2, 4}, {3, 4}};
		System.out.println(getCriticalNodes(links1, numLinks1, numRouters1));
		int numRouters2 = 5;
		int numLinks2 = 5;
		int[][] links2 = {{0, 1}, {1, 2}, {0, 2}, {0, 3}, {3, 4}};
		System.out.println(getCriticalNodes(links2, numLinks2, numRouters2));
		int numRouters3 = 4;
		int numLinks3 = 3;
		int[][] links3 = {{0, 1}, {1, 2}, {2, 3}};
		System.out.println(getCriticalNodes(links3, numLinks3, numRouters3));
		int numRouters4 = 7;
		int numLinks4 = 7;
		int[][] links4 = {{0, 1}, {0, 2}, {1, 3}, {2, 3}, {2, 5}, {5, 6}, {3, 4}};
		System.out.println(getCriticalNodes(links4, numLinks4, numRouters4));
		int numRouters5 = 4;
		int numLinks5 = 4;
		int[][] links5 = {{0, 1}, {0, 2}, {0, 3}};
		System.out.println(getCriticalNodes(links5, numLinks5, numRouters5));
	}

	private static List<Integer> getCriticalNodes(int[][] links, int numLinks, int numRouters) {
		time = 0;
		Map<Integer, Set<Integer>> map = new HashMap<>();
		for(int i=0;i<numRouters;i++) {
			map.put(i, new HashSet<>());
		}
		for(int[] link : links) {
			map.get(link[0]).add(link[1]);
			map.get(link[1]).add(link[0]);
		}
		Set<Integer> set = new HashSet<>();
		int[] low = new int[numRouters];
		int[] ids = new int[numRouters];
		int parent[] = new int[numRouters]; 
		Arrays.fill(ids, -1);
		Arrays.fill(parent, -1);
		for(int i=0;i<numRouters;i++) {
			if(ids[i] == -1)
				dfs(map, low, ids, parent, i, set);
		}
		return new ArrayList<>(set);
	}



	private static void dfs(Map<Integer, Set<Integer>> map, int[] low, int[] ids, int[] parent, int cur, Set<Integer> res) {
		int children = 0; 
		ids[cur] = low[cur]= ++time;
		for(int nei : map.get(cur)) {
			if(ids[nei] == -1) {
				children++;
				parent[nei] = cur;
				dfs(map, low, ids, parent,nei, res);
				low[cur] = Math.min(low[cur], low[nei]);
				if((parent[cur] == -1 && children > 1) || (parent[cur] != -1 && low[nei] >= ids[cur]))
					res.add(cur);
			}
			else if(nei != parent[cur])
				low[cur] = Math.min(low[cur], ids[nei]);
		}
	}
}

```
