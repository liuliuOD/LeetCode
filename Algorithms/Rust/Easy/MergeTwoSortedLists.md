## [Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists)

### Solution :

Method 1 :
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
impl Solution {
    pub fn merge_two_lists(list1: Option<Box<ListNode>>, list2: Option<Box<ListNode>>) -> Option<Box<ListNode>> {
        match (list1, list2) {
            (None, None) => None,
            (Some(node), None) | (None, Some(node)) => Some(node),
            (Some(node1), Some(node2)) => {
                if (node1.val > node2.val) {
                    Some(Box::new(ListNode {
                        next: Solution::merge_two_lists(Some(node1), node2.next),
                        val: node2.val,
                    }))
                } else {
                    Some(Box::new(ListNode {
                        next: Solution::merge_two_lists(node1.next, Some(node2)),
                        val: node1.val,
                    }))
                }
            }
        }
    }
}
```

Method 2 :
```rust
```
