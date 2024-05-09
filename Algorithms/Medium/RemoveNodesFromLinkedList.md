![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 2487. [Remove Nodes From Linked List](https://leetcode.com/problems/remove-nodes-from-linked-list)

### Solution :

```rust
// Definition for singly-linked list.
// #[derive(PartialEq, Eq, Clone, Debug)]
// pub struct ListNode {
//   pub val: i32,
//   pub next: Option<Box<ListNode>>
// }
//
// impl ListNode {
//   #[inline]
//   fn new(val: i32) -> Self {
//     ListNode {
//       next: None,
//       val
//     }
//   }
// }
```

Method 1 (Recursion, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```rust
impl Solution {
    pub fn remove_nodes(mut head: Option<Box<ListNode>>) -> Option<Box<ListNode>> {
        Self::recursion(head.as_mut());
        return head
    }

    fn recursion(node: Option<&mut Box<ListNode>>) -> i32 {
        match node {
            None => 0,
            Some(inner) => {
                if Self::recursion(inner.next.as_mut()) > inner.val {
                    *inner = inner.next.take().unwrap();
                }

                return inner.val
            },
        }
    }
}
```

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

Method 4 (Reverse, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def removeNodes(self, head: Optional[ListNode]) -> Optional[ListNode]:
        head_reverse = None
        while head:
            temp = head.next
            head.next = head_reverse
            head_reverse, head = head, temp

        maximum = head_reverse.val
        node = head_reverse
        while node and node.next:
            if node.next.val >= maximum:
                maximum = node.next.val
                node = node.next
            else:
                node.next = node.next.next

        head = None
        while head_reverse:
            temp = head_reverse.next
            head_reverse.next = head
            head, head_reverse = head_reverse, temp

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
