Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

## Example:

Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4

```java
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {	
// maintain an unchanging reference to node ahead of the return node.
		ListNode res = new ListNode(0);
		ListNode curr = res;
        
        while(l1 != null && l2 != null){
            if(l1.val <= l2.val){
                curr.next = l1;
                l1 = l1.next;
            }else{
                curr.next = l2;
                l2 = l2.next;
            }
            curr = curr.next;
        }
        // exactly one of l1 and l2 can be non-null at this point, so connect
        // the non-null list to the end of the merged list.
        curr.next = l1 == null? l2: l1;
        return res.next;      
    }

```
本题和上一题思路差不多。
有一点要注意，因为是sorted array，所以出现一个null的时候，另一个List依然是sorted。
所以可以直接加上去。
这样判定条件就可以少一点。

Time complexity : O(n+m)   

Because exactly one of l1 and l2 is incremented on each loop iteration, the while loop runs for a number of iterations equal to the sum of the lengths of the two lists. All other work is constant, so the overall complexity is linear.  

Space complexity : O(1)   
     
The iterative approach only allocates a few pointers, so it has a constant overall memory footprint.   
