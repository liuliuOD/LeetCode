![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2181. [Merge Nodes In Between Zeros](https://leetcode.com/problems/merge-nodes-in-between-zeros)

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

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn merge_nodes(mut head: Option<Box<ListNode>>) -> Option<Box<ListNode>> {
        if head.is_none() {
            return head
        }

        let mut node: Option<&mut ListNode> = head.as_deref_mut();
        while let Some(inner) = node.take() {
            match inner.next.take() {
                None => break,
                Some(mut inner_next) => {
                    if inner_next.val == 0 {
                        inner.next = inner_next.next.take();
                        node = inner.next.as_deref_mut();
                    } else {
                        inner.val += inner_next.val;
                        inner.next = inner_next.next;
                        node = Some(inner);
                    }
                },
            };
        }

        return head
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

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def mergeNodes(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if head is None:
            return head

        node_remaining = head
        node = head.next
        summarize = 0
        while node:
            summarize += node.val
            if node.val == 0 and summarize > 0:
                node_remaining.val = summarize
                summarize = 0
                if node.next:
                    node_remaining.next = node
                else:
                    node_remaining.next = None

                node_remaining = node

            node = node.next

        return head
```

Method 2 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def mergeNodes(self, head: Optional[ListNode]) -> Optional[ListNode]:
        if head is None:
            return head

        node_remaining = head
        node = head.next
        while node:
            node_remaining.val += node.val
            if node.val == 0 and node_remaining.val > 0:
                if node.next:
                    node_remaining.next = node
                else:
                    node_remaining.next = None

                node_remaining = node

            node = node.next

        return head
```
