![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 145. [Binary Tree Postorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal)

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

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(Log(N))$ (N: number of the nodes in the tree)) :
```Rust
use std::rc::Rc;
use std::cell::RefCell;
impl Solution {
    pub fn postorder_traversal(root: Option<Rc<RefCell<TreeNode>>>) -> Vec<i32> {
        return match root {
            None => vec![],
            Some(node) => {
                let mut result: Vec<i32> = vec![];
                if node.borrow().left.is_some() {
                    result.append(&mut Self::postorder_traversal(node.borrow().left.clone()));
                }

                if node.borrow().right.is_some() {
                    result.append(&mut Self::postorder_traversal(node.borrow().right.clone()));
                }

                result.push(node.borrow().val);

                return result
            }
        }
    }
}
```
