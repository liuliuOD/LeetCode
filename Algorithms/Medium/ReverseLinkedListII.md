![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 92. [Reverse Linked List II](https://leetcode.com/problems/swapping-nodes-in-a-linked-list)

### Solution :

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
```

Method 1 (Reverse Value) :
```python
class Solution:
    def reverseBetween(self, head: Optional[ListNode], left: int, right: int) -> Optional[ListNode]:
        head_dummy = ListNode(next=head)
        node_left = head_dummy
        for _ in range(left-1):
            node_left = node_left.next

        node_right = node_left
        values = [None] * (right-left+1)
        for index in range(right-left+1):
            node_right = node_right.next
            values[index] = node_right.val

        for value in reversed(values):
            node_left = node_left.next
            node_left.val = value

        return head_dummy.next
```

Method 2 (Reverse Nodes) :
```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseBetween(self, head: Optional[ListNode], left: int, right: int) -> Optional[ListNode]:
        head_dummy = ListNode(next=head)
        node_left = head_dummy
        for _ in range(left-1):
            node_left = node_left.next

        stack = []
        node_right = node_left
        for _ in range(right-left+1):
            node_right = node_right.next
            stack.append(node_right)

        node_tail = node_right.next
        while stack:
            node_right = stack.pop()
            node_left.next = node_right
            node_left = node_left.next
        node_left.next = node_tail

        return head_dummy.next
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

Method 1 (Replace Values) :
```php
class Solution {

    /**
     * @param ListNode $head
     * @param Integer $left
     * @param Integer $right
     * @return ListNode
     */
    function reverseBetween($head, $left, $right) {
        $temp = new ListNode(0, $head);
        for ($index=0; $index < $left; $index++) {
            $temp = $temp->next;
        }

        $values = $this->getValuesInRange($temp, $right-$left+1);

        foreach ($values as $value) {
            $temp->val = $value;
            $temp = $temp->next;
        }

        return $head;
    }

    function getValuesInRange($node, $offset) {
        $values = [];
        while ($offset) {
            $offset--;
            $values[] = $node->val;
            $node = $node->next;
        }

        return array_reverse($values);
    }
}
```
