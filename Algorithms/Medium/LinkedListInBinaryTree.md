![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1367. [Linked List In Binary Tree](https://leetcode.com/problems/linked-list-in-binary-tree)

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
// Definition for a binary tree node.
// #[derive(Debug, PartialEq, Eq)]
// pub struct TreeNode {
//   pub val: i32,
//   pub left: Option<Rc<RefCell<TreeNode>>>,
//   pub right: Option<Rc<RefCell<TreeNode>>>,
// }
//
// impl TreeNode {
//   #[inline]
//   pub fn new(val: i32) -> Self {
//     TreeNode {
//       val,
//       left: None,
//       right: None
//     }
//   }
// }
```

Method 1 (DFS, Time Complexity: $O(M*N)$, Space Complexity: $O(Log(M))$ (M: the number of the elements in the tree, N: the number of the elements in the linked list)) :
```rust

use std::rc::Rc;
use std::cell::RefCell;

type CustomNode = Box<ListNode>;
type CustomTree = Rc<RefCell<TreeNode>>;
impl Solution {
    pub fn is_sub_path(head: Option<CustomNode>, root: Option<CustomTree>) -> bool {
        if head.is_none() {
            return true
        }
        if root.is_none() {
            return false
        }

        return Self::traverse_tree(root.as_ref().unwrap(), head.as_ref().unwrap())
    }

    fn traverse_tree(root: &CustomTree, head: &CustomNode) -> bool {
        let mut result: bool = Self::is_connected(root, head);
        if !result && root.borrow().left.is_some() {
            result = Self::traverse_tree(root.borrow().left.as_ref().unwrap(), head);
        }
        if !result && root.borrow().right.is_some() {
            result = Self::traverse_tree(root.borrow().right.as_ref().unwrap(), head);
        }

        return result
    }

    fn is_connected(root: &CustomTree, head: &CustomNode) -> bool {
        if root.borrow().val != head.val {
            return false
        }

        if head.next.is_none() {
            return true
        }

        let mut result: bool = false;
        if root.borrow().left.is_some() {
            result |= Self::is_connected(root.borrow().left.as_ref().unwrap(), head.next.as_ref().unwrap());
        }
        if root.borrow().right.is_some() {
            result |= Self::is_connected(root.borrow().right.as_ref().unwrap(), head.next.as_ref().unwrap());
        }

        return result
    }
}
```
