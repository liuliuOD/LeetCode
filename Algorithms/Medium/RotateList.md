![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 61. [Rotate List](https://leetcode.com/problems/rotate-list)

### Solution :

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
```

Method 1 (Cycle then remove) :
```python
class Solution:
    def rotateRight(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        if k == 0 or head is None:
            return head

        node_amount = 1
        node = head
        while node.next:
            node = node.next
            node_amount += 1
        # set list to cycle
        node.next = head

        k = k % node_amount
        node = head
        for _ in range(node_amount - k):
            tail = node
            node = node.next
        tail.next = None

        return node
```

Method 2 :
```python
class Solution:
    def rotateRight(self, head: Optional[ListNode], k: int) -> Optional[ListNode]:
        if k == 0 or head is None:
            return head

        node_amount = 1
        node = head
        while node.next:
            node = node.next
            node_amount += 1
        # set list to cycle
        node.next = head

        k = k % node_amount
        node = head
        for _ in range(node_amount - k - 1):
            node = node.next
        result, node.next = node.next, None

        return result
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

Method 1 (Cycle + Fast & Slow Pointer) :
```php
class Solution {

    /**
     * @param ListNode $head
     * @param Integer $k
     * @return ListNode
     */
    function rotateRight($head, $k) {
        if (is_null($head)) {
            return NULL;
        }

        $dummyHead = $node = new ListNode(0, $head);
        $amountNode = 0;
        while ($node->next) {
            $node = $node->next;
            $amountNode++;
        }
        $tail = $node;

        $fast = $slow = $dummyHead;
        for ($_ = 0; $_ < $k%$amountNode; $_++) {
            $fast = $fast->next;
        }
        while ($fast->next) {
            $fast = $fast->next;
            $slow = $slow->next;
        }
        $tail->next = $head;
        $result = $slow->next;
        $slow->next = NULL;

        return $result;
    }
}
```

Method 2 (Cycle) :
```php
class Solution {

    /**
     * @param ListNode $head
     * @param Integer $k
     * @return ListNode
     */
    function rotateRight($head, $k) {
        if (is_null($head)) {
            return NULL;
        }

        $dummyHead = new ListNode(0, $head);

        $amountNode = 0;
        $node = $dummyHead;
        while ($node->next) {
            $node = $node->next;
            $amountNode++;
        }
        $tail = $node;

        $node = $dummyHead;
        for ($_ = 0; $_ < ($amountNode - $k%$amountNode); $_++) {
            $node = $node->next;
        }
        $tail->next = $head;
        $result = $node->next;
        $node->next = NULL;

        return $result;
    }
}
```
