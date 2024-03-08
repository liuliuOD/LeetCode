![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 206. [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list)

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

Method 1 (Dummy Pointer) :
```rust
impl Solution {
    pub fn reverse_list(head: Option<Box<ListNode>>) -> Option<Box<ListNode>> {
        let mut result: Option<Box<ListNode>> = None;
        let mut current: Option<Box<ListNode>> = head;
        while let Some(mut node) = current {
            current = node.next;
            /* Option 1 */
            node.next = result;
            /* Option 2

            node.next = result.take();
            */
            result = Some(node);
        }

        return result
    }
}
```

Method 2 :
```rust
impl Solution {
    pub fn reverse_list(mut head: Option<Box<ListNode>>) -> Option<Box<ListNode>> {
        let mut result: Option<Box<ListNode>> = None;
        while let Some(mut node) = head {
            /* Option 1 */
            head = node.next;
            node.next = result.take();
            /* Option 2

            head = std::mem::replace(&mut node.next, result.take());
            */
            result = Some(node);
        }

        return result
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
