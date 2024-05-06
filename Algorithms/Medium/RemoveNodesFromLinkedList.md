![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 2487. [Remove Nodes From Linked List](https://leetcode.com/problems/remove-nodes-from-linked-list)

### Solution :

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
```

Method 1 (Monotonic Stack, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def removeNodes(self, head: Optional[ListNode]) -> Optional[ListNode]:
        stack = []
        node = ListNode(next=head)
        while node:
            while stack and stack[-1] < node.val:
                stack.pop()

            stack.append(node.val)
            node = node.next

        node = dummyNode = ListNode(next=head)
        for node_val in stack:
            node.next = ListNode(val=node_val)
            node = node.next

        return dummyNode.next
```

Method 2 (Monotonic Stack + Queue, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def removeNodes(self, head: Optional[ListNode]) -> Optional[ListNode]:
        monotonic = deque([])
        while head:
            while monotonic and monotonic[-1] < head.val:
                monotonic.pop()
            monotonic.append(head.val)
            head = head.next

        dummy = ListNode()
        node = dummy
        while monotonic:
            node.next = ListNode(val=monotonic.popleft())
            node = node.next

        return dummy.next
```

Method 3 (Recursion, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def removeNodes(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if head is None or head.next is None:
            return head

        node_next = self.removeNodes(head.next)

        if head.val < node_next.val:
            return node_next

        head.next = node_next
        return head
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

Method 1 (Reverse) :
```php
class Solution {

    /**
     * @param ListNode $head
     * @return ListNode
     */
    function removeNodes($head) {
        $headReversed = $this->reverseNodes($head);

        $dummyHead = new ListNode(0, $headReversed);
        $node = $dummyHead;
        while ($node->next) {
            if ($node->val > $node->next->val) {
                $node->next = $node->next->next;
            } else {
                $node = $node->next;
            }
        }

        return $this->reverseNodes($dummyHead->next);
    }

    function reverseNodes($head) {
        $dummyHead = new ListNode(0, $head);
        $current = $dummyHead->next;
        while($current->next) {
            $next = $current->next;
            $current->next = $next->next;
            $next->next = $dummyHead->next;
            $dummyHead->next = $next;
        }

        return $dummyHead->next;
    }
}
```

Method 2 (Monotonic Stack) :
```php
class Solution {

    /**
     * @param ListNode $head
     * @return ListNode
     */
    function removeNodes($head) {
        $stack = [];
        $node = new ListNode(0, $head);
        while($node) {
            while(count($stack) && end($stack) < $node->val) {
                array_pop($stack);
            }
            $stack[] = $node->val;
            $node = $node->next;
        }

        $node = $result = new ListNode();
        foreach($stack as $value) {
            $node->next = new ListNode($value);
            $node = $node->next;
        }

        return $result->next;
    }
}
```

### Solution :

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
```

Method 1 (Recursion, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```go
func removeNodes(head *ListNode) *ListNode {
    if head == nil || head.Next == nil {
        return head
    }

    node_next := removeNodes(head.Next)

    if head.Val < node_next.Val {
        return node_next
    }
    head.Next = node_next

    return head
}
```
