![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3217. [Delete Nodes From Linked List Present In Array](https://leetcode.com/problems/delete-nodes-from-linked-list-present-in-array)

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

Method 1 (Hash Set, Time Complexity: $O(M+N)$, Space Complexity: $O(N)$ (M: amount of the nodes in the tree, N: number of the elements in `nums`)) :
```rust
use std::collections::HashSet;
type Custom = Option<Box<ListNode>>;

impl Solution {
    pub fn modified_list(nums: Vec<i32>, mut head: Custom) -> Custom {
        let set: HashSet<i32> = HashSet::from_iter(nums.into_iter());
        let mut dummy: ListNode = ListNode::new(0);
        let mut current: &mut ListNode = &mut dummy;
        while let Some(mut inner) = head {
            if set.contains(&inner.val) {
                head = inner.next;
            } else {
                head = inner.next.take();
                current.next = Some(inner);
                if current.next.is_none() {
                    break;
                }

                current = current.next.as_mut().unwrap();
            }
        }

        return dummy.next
    }
}
```
