![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 876. [Middle Of The Linked List](https://leetcode.com/problems/middle-of-the-linked-list)

### Solution :

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
```

Method 1 (Slow & Fast Pointers, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def middleNode(self, head: Optional[ListNode]) -> Optional[ListNode]:
        pointer_slow = head
        pointer_fast = head
        while pointer_fast and pointer_fast.next:
            pointer_slow = pointer_slow.next
            pointer_fast = pointer_fast.next.next
        return pointer_slow
```

Method 2 (Slow & Fast Pointers, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def middleNode(self, head: Optional[ListNode]) -> Optional[ListNode]:
        dummy = ListNode(next=head)
        slow = fast = dummy
        while fast:
            fast = fast.next
            if fast:
                fast = fast.next
            slow = slow.next

        return slow
```

### Solution :

```php
/**
 * Definition for a singly-linked list.
 * class ListNode {
 *     public $val = 0;
 *     public $next = null;
 *     function __construct($val = 0, $next = null) {
 *         $this->val = $val;
 *         $this->next = $next;
 *     }
 * }
 */
```

Method 1 (Slow & Fast Pointers + Dummy Pointer) :
```php
class Solution {

    /**
     * @param ListNode $head
     * @return ListNode
     */
    function middleNode($head) {
        $slow = $fast = new ListNode(0, $head);

        while ($fast) {
            $slow = $slow->next;
            if ($fast->next == null) {
                return $slow;
            }

            $fast = $fast->next->next;
        }

        return $slow;
    }
}
```
