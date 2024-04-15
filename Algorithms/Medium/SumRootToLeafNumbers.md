![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 129. [Sum Root To Leaf Numbers](https://leetcode.com/problems/sum-root-to-leaf-numbers)

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

Method 1 (Recursive Traversal, Time Complexity: $O(N)$, Space Complexity: $O(D)$ (D: depth of the tree)) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
impl Solution {
    pub fn sum_numbers(root: Option<Rc<RefCell<TreeNode>>>) -> i32 {
        return Self::traverse(root.clone(), 0)
    }

    fn traverse(node: Option<Rc<RefCell<TreeNode>>>, current: i32) -> i32 {
        return match node {
            None => 0,
            Some(node) => {
                let current: i32 = current*10 + node.borrow().val;
                let mut result: i32 = 0;
                if node.borrow().left.is_none() && node.borrow().right.is_none() {
                    return current
                }

                if node.borrow().left.is_some() {
                    result += Self::traverse(node.borrow().left.clone(), current);
                }
                if node.borrow().right.is_some() {
                    result += Self::traverse(node.borrow().right.clone(), current);
                }
                return result
            },
        }
    }
}
```
