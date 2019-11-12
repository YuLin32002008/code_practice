
A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.  
Return a deep copy of the list.  
Input:  
{"$id":"1","next":{"$id":"2","next":null,"random":{"$ref":"2"},"val":2},"random":{"$ref":"2"},"val":1}  
  
Explanation:  
Node 1's value is 1, both of its next and random pointer points to Node 2.  
Node 2's value is 2, its next pointer points to null and its random pointer points to itself.  

## Solution1: Recursive -- treat it like a graph
```java
class Node {
    public int val;
    public Node next;
    public Node random;

    public Node() {}

    public Node(int _val,Node _next,Node _random) {
        val = _val;
        next = _next;
        random = _random;
    }
};

public class CopyListwithRandomPointer {
	
	HashMap<Node, Node> visitedHash = new HashMap<>();
	
	public Node copyRandomList(Node head) {
        
        if(head == null){
        	return null;
        }
		
        //if visited, return it
        if(this.visitedHash.containsKey(head)){
        	return visitedHash.get(head);
        }
        
        //if not visited, copy the node and save it in hashmap
        Node node = new Node(head.val,null,null);
        // Save this value in the hash map. This is needed since there might be
        // loops during traversal due to randomness of random pointers and this would help us avoid
        // them.
        this.visitedHash.put(head, node);
        
        node.next = copyRandomList(head.next);
        node.random = copyRandomList(head.random);
        
        return node;  
    }
}
```
用递归的方法去解决。为了避免进入死循环，所以将访问过的结点放入一个哈希表。     
Time Complexity: O(N)O(N) where N is the number of nodes in the linked list.     
Space Complexity: O(N)O(N). If we look closely, we have the recursion stack and we also have the space complexity to keep track of nodes already cloned i.e. using the visited dictionary. But asymptotically, the complexity is O(N)O(N). 

## Solution2: iterate in O(n) time -- treat it like a linked list
```java
public class CopyListwithRandomPointer {
	
	HashMap<Node, Node> visitedHash = new HashMap<>();
	
	public Node getRandomList(Node node){
		if(node == null){
			return null;
		}
		
		if(this.visitedHash.containsKey(node)){
			return this.visitedHash.get(node);
		}else{
			this.visitedHash.put(node, new Node(node.val, null, null));
			return this.visitedHash.get(node);
		}
		
	}
	
	public Node copyRandomList(Node head) {
		if (head == null) {
		      return null;
		    }
		
        Node newList = new Node(head.val, null, null);
        Node oldList = head;
        
        this.visitedHash.put(oldList, newList);
        
        while(oldList!= null){
        	newList.next = getRandomList(oldList.next);
        	newList.random = getRandomList(oldList.random);
        	
        	oldList = oldList.next;
        	newList = newList.next;
        }
        return this.visitedHash.get(head);
        
    }
}
```
最后Return的是this.visitedHash.get(head), 而不是newList，因为此时newList是null。   
The key of this question is using a separate dictionary to keep the old node --> new node mapping.      
Time Complexity : O(N) because we make one pass over the original linked list.      
Space Complexity : O(N) as we have a dictionary containing mapping from old list nodes to new list nodes. Since there are NN nodes, we have O(N)O(N) space complexity.       

## Solution3: iterate with O(1) space.
```java
public class CopyListwithRandomPointer {
	
	public Node copyRandomList(Node head) {
		if(head == null){
			return null;
		}
		
		Node weaved = head;
		Node temp = new Node();
		while (weaved != null){
			temp = weaved.next;
			weaved.next = new Node(weaved.val,null,null);
			weaved.next.next = temp;
			weaved = weaved.next.next;
		}
		
		weaved = head;
		
		while(weaved != null){
			weaved.next.random = (weaved.random == null) ? null : weaved.random.next;
			weaved = weaved.next.next;
		}
		
		Node old_list = head;
		Node new_list = head.next;
		Node new_node = head.next;
		
		while(old_list != null){
			old_list.next = old_list.next.next;
			new_list.next = (new_list.next == null) ? null : new_list.next.next;
			old_list = old_list.next;
			new_list = new_list.next;
		}
		
		return new_node;
		      
    }
}
```
bralliant idea! 把原来的链表拓宽为两倍。 然后重新拼接。 学习到了。    
Time Complexity : O(N)       
Space Complexity : O(1)            
