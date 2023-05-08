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
