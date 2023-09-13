![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 206. [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list)

### Solution :

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
```

Method 1 (Dummy Pointer) :
```python
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if head is None:
            return head

        dummy = ListNode()
        cur = head
        while cur:
            temp = cur.next
            cur.next = dummy
            cur, dummy = temp, cur

        head.next = None
        return dummy
```

Method 2 (Dummy Pointer) :
```python
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        dummy = None
        cur = head
        while cur:
            temp = cur.next
            cur.next = dummy
            cur, dummy = temp, cur

        return dummy
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

Method 1 (Recursive) :
```php
class Solution {
    protected $headReverse;

    /**
     * @param ListNode $head
     * @return ListNode
     */
    function reverseList($head) {
        $this->reverse(null, $head);

        return $this->headReverse;
    }

    function reverse($previous, $current) {
        if ($current == null) {
            return null;
        } else if ($current->next == null) {
            $this->headReverse = $current;
        } else {
            $this->reverse($current, $current->next);
        }

        $current->next = $previous;
    }
}
```

Method 2 (Dummy Pointer) :
```php
class Solution {

    /**
     * @param ListNode $head
     * @return ListNode
     */
    function reverseList($head) {
        $previous = null;
        $current = $head;
        while($current) {
            $temp = $current->next;
            $current->next = $previous;
            $previous = $current;
            $current = $temp;
        }

        return $previous;
    }
}
```

Method 3 (Dummy Pointer) :
```php
class Solution {

    /**
     * @param ListNode $head
     * @return ListNode
     */
    function reverseList($head) {
        $nodeDummy = new ListNode(0, $head);
        $nodeCurrent = $nodeDummy->next;
        while($nodeCurrent->next) {
            $nodeNext = $nodeCurrent->next;
            $nodeCurrent->next = $nodeNext->next;
            $nodeNext->next = $nodeDummy->next;
            $nodeDummy->next = $nodeNext;
        }

        return $nodeDummy->next;
    }
}
```
