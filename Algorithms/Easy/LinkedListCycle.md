![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 141. [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle)

### Solution :

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None
```

Method 1 (Slow & Fast Pointers) :
```python
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        dummy = ListNode(None)
        dummy.next = head
        pointer_slow = pointer_fast = dummy
        while pointer_fast:
            pointer_slow = pointer_slow.next
            pointer_fast = pointer_fast.next
            if pointer_fast is None:
                break
            pointer_fast = pointer_fast.next

            if pointer_fast == pointer_slow:
                return True
        return False
```

Method 2 (Slow & Fast Pointers) :
```python
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        pointer_slow = pointer_fast = head
        while pointer_fast and pointer_fast.next:
            pointer_slow = pointer_slow.next
            pointer_fast = pointer_fast.next.next

            if pointer_fast == pointer_slow:
                return True
        return False
```

Method 2 (Slow & Fast Pointers, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        dummy = ListNode(0)
        dummy.next = head
        slow = fast = dummy
        while fast.next and fast.next.next:
            fast = fast.next.next
            slow = slow.next
            if fast == slow:
                return True

        return False
```

### Solution :

```php
/**
 * Definition for a singly-linked list.
 * class ListNode {
 *     public $val = 0;
 *     public $next = null;
 *     function __construct($val) { $this->val = $val; }
 * }
 */
```

Method 1 (Slow & Fast Pointers) :
```php
class Solution {
    /**
     * @param ListNode $head
     * @return Boolean
     */
    function hasCycle($head) {
        $slow = $fast = new ListNode(0);
        $slow->next = $head;

        while ($fast && $fast->next) {
            $slow = $slow->next;
            $fast = $fast->next->next;

            if ($slow === $fast) {
                return true;
            }
        }

        return false;
    }
}
```

Method 2 (Hash Table) :
```php
class Solution {
    /**
     * @param ListNode $head
     * @return Boolean
     */
    function hasCycle($head) {
        $mapping = [];
        while ($head) {
            // used third parameter to valid type
            if (in_array($head, $mapping, true)) {
                return true;
            }

            $mapping[] = $head;
            $head = $head->next;
        }

        return false;
    }
}
```
