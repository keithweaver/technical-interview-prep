```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
// Test Case:
// []
// [1] -> [2]
// [1] -> [2] -> [1]
// [1] -> [2] -> [3]
class Solution {
    public ListNode reverseList(ListNode head) {
        if (head == null || head.next == null){
            return head;
        }
        ListNode reverseFromNextNode = reverseList(head.next);
        head.next.next = head;
        head.next = null;
        return reverseFromNextNode;
    }
}
```
