![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 1721. [Swapping Nodes In A Linked List](https://leetcode.com/problems/swapping-nodes-in-a-linked-list)

### Solution :

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
```

Method 1 (Slow & Fast Pointers) :
```python
class Solution:
    def swapNodes(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        pointer_dummy = ListNode(0, head)
        pointer_slow = pointer_dummy
        pointer_fast = pointer_dummy

        pointer_fast = self.traverse(pointer_fast, k)
        pointer_left = pointer_fast

        while pointer_fast:
            pointer_slow = self.traverse(pointer_slow, 1)
            pointer_fast = self.traverse(pointer_fast, 1)

        (pointer_left.val, pointer_slow.val) = (pointer_slow.val, pointer_left.val)

        return head

    def traverse(self, pointer, k) -> Optional[ListNode]:
        for _ in range(0, k):
            pointer = pointer.next
        return pointer
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

Method 1 (Slow & Fast Pointers + Swap Nodes) :
```php
class Solution {

    /**
     * @param ListNode $head
     * @param Integer $k
     * @return ListNode
     */
    function swapNodes($head, $k) {
        $beginning = null;
        $dummy = $end = $temp = new ListNode(0, $head);

        for ($index=1; $index < $k; $index++) {
            $temp = $temp->next;
        }
        $beginning = $temp;

        while ($temp->next && $temp->next->next) {
            $temp = $temp->next;
            $end = $end->next;
        }

        $nodeBeginning = $beginning->next;
        $nodeEnd = $end->next;
        $beginning->next = $nodeEnd;
        $end->next = $nodeBeginning;
        $nodeEndNext = $nodeEnd->next;
        $nodeEnd->next = $nodeBeginning->next;
        $nodeBeginning->next = $nodeEndNext;

        return $dummy->next;
    }
}
```

Method 2 (Slow & Fast Pointers + Swap Values) :
```php
class Solution {

    /**
     * @param ListNode $head
     * @param Integer $k
     * @return ListNode
     */
    function swapNodes($head, $k) {
        $beginning = null;
        $end = $head;
        $dummy = $temp = new ListNode(0, $head);

        for ($index=0; $index < $k; $index++) {
            $temp = $temp->next;
        }
        $beginning = $temp;

        while ($temp->next) {
            $temp = $temp->next;
            $end = $end->next;
        }

        $tempValue = $beginning->val;
        $beginning->val = $end->val;
        $end->val = $tempValue;

        return $dummy->next;
    }
}
```
