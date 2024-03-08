![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 203. [Remove Linked List Elements](https://leetcode.com/problems/remove-linked-list-elements)

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

Method 1 (Dummy + move ownership) :
```rust
impl Solution {
    pub fn remove_elements(mut head: Option<Box<ListNode>>, val: i32) -> Option<Box<ListNode>> {
        let mut dummy = None;
        let mut dummy_tail = &mut dummy;
        while let Some(mut node) = head.take() {
            head = node.next.take();

            if node.val == val {
                continue;
            }

            *dummy_tail = Some(node);
            dummy_tail = &mut dummy_tail.as_mut().unwrap().next;
        }

        return dummy
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

Method 1 (Dummy) :
```python
class Solution:
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        dummy = ListNode(None)
        dummy.next = head
        node = dummy
        while node and node.next:
            if node.next.val == val:
                node.next = node.next.next
                continue
            node = node.next

        return dummy.next
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

Method 1 :
```php
class Solution {

    /**
     * @param ListNode $head
     * @param Integer $val
     * @return ListNode
     */
    function removeElements($head, $val) {
        $node = $dummyHead = new ListNode(NULL, $head);
        while($node->next) {
            if ($node->next->val == $val) {
                $node->next = $node->next->next;
            } else {
                $node = $node->next;
            }
        }

        return $dummyHead->next;
    }
}
```
