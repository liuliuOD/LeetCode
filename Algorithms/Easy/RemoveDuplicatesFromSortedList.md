![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## [Remove Duplicates From Sorted List](https://leetcode.com/problems/remove-duplicates-from-sorted-list)

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

Method 1 :
```rust
impl Solution {
    pub fn delete_duplicates(mut head: Option<Box<ListNode>>) -> Option<Box<ListNode>> {
        if let Some(mut node) = head.as_mut() {
            while let Some(node_next) = node.next.as_mut() {
                if node.val == node_next.val {
                    node.next = node_next.next.take();
                    continue;
                }
                node = node.next.as_mut().unwrap();
            }
        }

        head
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

Method 1 :
```python
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        node = head
        while node:
            if node.next and node.val == node.next.val:
                node.next = node.next.next
                continue
            node = node.next

        return head
```
