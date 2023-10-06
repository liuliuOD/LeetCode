![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 2095. [Delete The Middle Node Of A Linked List](https://leetcode.com/problems/delete-the-middle-node-of-a-linked-list)

### Solution :

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
```

Method 1 (Slow & Fast Pointer + Dummy Head) :
```python
class Solution:
    def deleteMiddle(self, head: Optional[ListNode]) -> Optional[ListNode]:
        slow = fast = dummyHead = ListNode(next=head)
        while fast:
            if not fast.next or not fast.next.next:
                slow.next = slow.next.next
                break

            fast = fast.next.next
            slow = slow.next

        return dummyHead.next
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

Method 1 (Slow & Fast Pointer + Dummy Head) :
```php
class Solution {

    /**
     * @param ListNode $head
     * @return ListNode
     */
    function deleteMiddle($head) {
        $slow = $fast = $dummyHead = new ListNode(NULL, $head);
        while($fast) {
            if (is_null($fast->next) || is_null($fast->next->next)) {
                $slow->next = $slow->next->next;
                break;
            }
            $fast = $fast->next->next;
            $slow = $slow->next;
        }

        return $dummyHead->next;
    }
}
```
