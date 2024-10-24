![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 951. [Flip Equivalent Binary Trees](https://leetcode.com/problems/flip-equivalent-binary-trees)

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

Method 1 (DFS, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of the elements in the smaller tree)) :
```rust
use std::rc::Rc;
use std::cell::RefCell;

type Custom = Rc<RefCell<TreeNode>>;
impl Solution {
    pub fn flip_equiv(root1: Option<Custom>, root2: Option<Custom>) -> bool {
        return Self::dfs(root1.clone(), root2.clone())
    }

    fn dfs(node1: Option<Custom>, node2: Option<Custom>) -> bool {
        if node1.is_none() && node2.is_none() {
            return true
        } else if node1.is_none() || node2.is_none() {
            return false
        } else if node1.clone().unwrap().borrow().val != node2.clone().unwrap().borrow().val {
            return false
        }

        return (
                Self::dfs(node1.clone().unwrap().borrow().left.clone(), node2.clone().unwrap().borrow().left.clone())
                && Self::dfs(node1.clone().unwrap().borrow().right.clone(), node2.clone().unwrap().borrow().right.clone())
            )
            || (
                Self::dfs(node1.clone().unwrap().borrow().left.clone(), node2.clone().unwrap().borrow().right.clone())
                && Self::dfs(node1.clone().unwrap().borrow().right.clone(), node2.clone().unwrap().borrow().left.clone())
            )
    }
}
```
