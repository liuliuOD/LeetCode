![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 979. [Distribute Coins In Binary Tree](https://leetcode.com/problems/distribute-coins-in-binary-tree)

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

Method 1 (DFS) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
type Custom = Option<Rc<RefCell<TreeNode>>>;
impl Solution {
    pub fn distribute_coins(root: Custom) -> i32 {
        let mut result: i32 = 0;
        Self::dfs(root.clone(), &mut result);
        return result
    }

    fn dfs(node: Custom, result: &mut i32) -> i32 {
        return match node {
            None => 0,
            Some(inner) => {
                let mut inner = inner.borrow_mut();
                if inner.left.is_some() {
                    inner.val += Self::dfs(inner.left.clone(), result);
                }
                if inner.right.is_some() {
                    inner.val += Self::dfs(inner.right.clone(), result);
                }

                *result += (inner.val-1).abs();
                return inner.val - 1
            },
        }
    }
}
```

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (DFS) :
```python
class Solution:
    def distributeCoins(self, root: Optional[TreeNode]) -> int:
        self.result = 0
        self.dfs(root)
        return self.result

    def dfs(self, node) -> int:
        if node.left:
            node.val += self.dfs(node.left)
        if node.right:
            node.val += self.dfs(node.right)

        self.result += abs(node.val - 1)
        return node.val - 1
```
