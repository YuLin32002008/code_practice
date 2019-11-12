Input:  
userSongs = {    
   "David": ["song1", "song2", "song3", "song4", "song8"],  
   "Emma":  ["song5", "song6", "song7"]  
},  
songGenres = {    
   "Rock":    ["song1", "song3"],  
   "Dubstep": ["song7"],  
   "Techno":  ["song2", "song4"],  
   "Pop":     ["song5", "song6"],  
   "Jazz":    ["song8", "song9"]  
}  
  
Output: {    
   "David": ["Rock", "Techno"],  
   "Emma":  ["Pop"]  
}  
  
Explanation:  
David has 2 Rock, 2 Techno and 1 Jazz song. So he has 2 favorite genres.  
Emma has 2 Pop and 1 Dubstep song. Pop is Emma's favorite genre.  
  



```java
// "static void main" must be defined in a public class.

import java.util.ArrayList;
import java.util.Arrays;
import java.util.HashMap;
import java.util.List;
import java.util.Map;


// Approach is simple: initialize a mapping of songsToGenre.
// Then, using our mapping, we iterate through each song 
// (we don't know if songs have multiple genres, so we handle that here), 
// and count up the genres while keeping a 'maximum count'.
// After that, we find out all of the songs that are equal to our maximum mapping. 

class Solution {
	public Map<String, List<String>> favoriteGenre(Map<String, List<String>> userMap, Map<String, 
	List<String>> genreMap) {
   	Map<String, List<String>> res = new HashMap<>();
   	Map<String, String> songstogenre = new HashMap<>();
   	
   	for(String genre : genreMap.keySet()) {
   		List<String> songs = genreMap.get(genre);
   		for(String song : songs) {
   			songstogenre.put(song, genre);
   		}
   	}
       Map<String, Integer> count = new HashMap();
   	int max = 0;
   	for(String user : userMap.keySet()) {
           count = new HashMap();
           max = 0;
           res.put(user, new ArrayList());
   		List<String> songs = userMap.get(user);
   		for(String song : songs) {
   			String genre = songstogenre.get(song);
   			int c = count.getOrDefault(genre, 0) + 1;
   			count.put(genre, c);
               max = Math.max(c, max);
   		}
           for (String key : count.keySet()) {
               if (count.get(key) == max) {
                   res.get(user).add(key);
               }
           }
   	}
   	return res;
   }
}


public class Main {
    public static void main(String[] args) {
        Map<String, List<String>> userMap = new HashMap<>();
		List<String> list1 = Arrays.asList("song1", "song2", "song3", "song4", "song8");
		List<String> list2 = Arrays.asList("song5", "song6", "song7");
		userMap.put("David", list1);
		userMap.put("Emma", list2);
		
		Map<String, List<String>> genreMap = new HashMap<>();
		List<String> list3 = Arrays.asList("song1", "song3");
		List<String> list4 = Arrays.asList("song7");
		List<String> list5 = Arrays.asList("song2", "song4");
		List<String> list6 = Arrays.asList("song5", "song6");
		List<String> list7 = Arrays.asList("song8", "song9");
		genreMap.put("Rock", list3);
		genreMap.put("Dubstep", list4);
		genreMap.put("Techno", list5);
		genreMap.put("Pop", list6);
		genreMap.put("Jazz", list7);
        
        /*Map<String, List<String>> userMap = new HashMap<>();
		List<String> list1 = Arrays.asList("song1", "song2");
		List<String> list2 = Arrays.asList("song3", "song4");
		userMap.put("David", list1);
		userMap.put("Emma", list2);
		
		Map<String, List<String>> genreMap = new HashMap<>();*/
        
        System.out.println(new Solution().favoriteGenre(userMap, genreMap));
    }
}

```
