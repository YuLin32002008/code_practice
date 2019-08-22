Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

## Example:

Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4

```java
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {				
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
        
        curr.next = l1 == null? l2: l1;
        return res.next;      
    }

```
本题和上一题思路差不多。
有一点要注意，因为是sorted array，所以出现一个null的时候，另一个List依然是sorted。
所以可以直接加上去。
这样判定条件就可以少一点。
