![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 2. [Add Two Numbers](https://leetcode.com/problems/add-two-numbers)

### Solution :

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
```

Method 1 (Traverse) :
```python
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        head = ListNode()
        current = head
        carry = 0
        while l1 or l2 or carry:
            if not l1:
                l1 = ListNode()
            if not l2:
                l2 = ListNode()
            val = carry + l1.val + l2.val
            carry = val // 10
            current.next = ListNode(val=val%10)
            current = current.next
            l1 = l1.next
            l2 = l2.next
        return head.next
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

Method 1 (Traverse) :
```php
class Solution {

    /**
     * @param ListNode $l1
     * @param ListNode $l2
     * @return ListNode
     */
    function addTwoNumbers($l1, $l2) {
        $dummyHead = $node = new ListNode();
        $carry = 0;
        while ($l1 || $l2 || $carry) {
            $current = $carry;
            if ($l1) {
                $current += $l1->val;
                $l1 = $l1->next;
            }
            if ($l2) {
                $current += $l2->val;
                $l2 = $l2->next;
            }

            $node->next = new ListNode($current % 10);
            $node = $node->next;
            $carry = intval($current / 10);
        }

        return $dummyHead->next;
    }
}
```
