![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 19. [Remove Nth Node From End Of List](https://leetcode.com/problems/add-two-numbers)

### Solution :

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
```

Method 1 (Slow & Fast Pointer) :
```python
class Solution:
    def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        dummy = ListNode(next=head)
        pointer_slow = dummy
        pointer_fast = dummy
        for i in range(n):
            pointer_fast = pointer_fast.next
        while pointer_fast.next:
            pointer_fast = pointer_fast.next
            pointer_slow = pointer_slow.next
        pointer_slow.next = pointer_slow.next.next
        return dummy.next
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

Method 1 (Slow & Fast Pointer) :
```php
class Solution {

    /**
     * @param ListNode $head
     * @param Integer $n
     * @return ListNode
     */
    function removeNthFromEnd($head, $n) {
        $dummyHead = $nodeSlow = $nodeFast = new ListNode(0, $head);
        for ($_ = 0; $_ < $n; $_++) {
            $nodeFast = $nodeFast->next;
        }

        while ($nodeFast->next) {
            $nodeFast = $nodeFast->next;
            $nodeSlow = $nodeSlow->next;
        }

        $nodeSlow->next = $nodeSlow->next->next;

        return $dummyHead->next;
    }
}
```
