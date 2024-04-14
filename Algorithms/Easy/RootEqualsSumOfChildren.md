![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2236. [Root Equals Sum Of Children](https://leetcode.com/problems/root-equals-sum-of-children)

### Solution :

```rust
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

Method 1 (Time Complexity: $O(1)$, Space Complexity: $O(1)$) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
impl Solution {
    pub fn check_tree(root: Option<Rc<RefCell<TreeNode>>>) -> bool {
        /* Option 1 */
        let node = root.as_ref().unwrap().borrow();
        let val_left: i32 = node.left.as_ref().unwrap().borrow().val;
        let val_right: i32 = node.right.as_ref().unwrap().borrow().val;
        return node.val == val_left+val_right
        /* Option 2

        return root.as_ref().unwrap().borrow().val == root.as_ref().unwrap().borrow().left.as_ref().unwrap().borrow().val + root.as_ref().unwrap().borrow().right.as_ref().unwrap().borrow().val
        */
        /* Option 3

        return match root {
            None => true,
            Some(node) => {
                node.borrow().val == node.borrow().left.as_ref().unwrap().borrow().val + node.borrow().right.as_ref().unwrap().borrow().val
            }
        }
        */
    }
}
```
