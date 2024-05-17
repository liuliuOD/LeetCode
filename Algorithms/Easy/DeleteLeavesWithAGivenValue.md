![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1325. [Delete Leaves With A Given Value](https://leetcode.com/problems/delete-leaves-with-a-given-value)

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

Method 1 (DFS, Time Complexity: $O(N)$, Space Complexity: $O(D)$ (D: depth of the tree)) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
type Custom = Option<Rc<RefCell<TreeNode>>>;
impl Solution {
    pub fn remove_leaf_nodes(root: Custom, target: i32) -> Custom {
        let remove: bool = Self::dfs(root.clone(), target);
        return match remove {
            true => None,
            false => root,
        }
    }

    fn dfs(node: Custom, target: i32) -> bool {
        if let Some(inner) = node {
            if inner.borrow().left.is_some() && Self::dfs(inner.borrow().left.clone(), target) {
                inner.borrow_mut().left = None;
            }

            if inner.borrow().right.is_some() && Self::dfs(inner.borrow().right.clone(), target) {
                inner.borrow_mut().right = None;
            }

            if inner.borrow().left.is_none() && inner.borrow().right.is_none() && inner.borrow().val == target {
                return true
            }
        }

        return false
    }
}
```

Method 2 (DFS, Time Complexity: $O(N)$, Space Complexity: $O(D)$ (D: depth of the tree)) :
```rust
use std::rc::Rc;
use std::cell::{RefMut, RefCell};
type Custom = Option<Rc<RefCell<TreeNode>>>;
impl Solution {
    pub fn remove_leaf_nodes(root: Custom, target: i32) -> Custom {
        let remove: bool = Self::dfs(root.clone(), target);
        return match remove {
            true => None,
            false => root,
        }
    }

    fn dfs(node: Custom, target: i32) -> bool {
        if let Some(inner) = node {
            let mut inner: RefMut<'_, TreeNode> = inner.borrow_mut();
            if inner.left.is_some() && Self::dfs(inner.left.clone(), target) {
                inner.left = None;
            }

            if inner.right.is_some() && Self::dfs(inner.right.clone(), target) {
                inner.right = None;
            }

            if inner.left.is_none() && inner.right.is_none() && inner.val == target {
                return true
            }
        }

        return false
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

Method 1 (DFS, Time Complexity: $O(N)$, Space Complexity: $O(D)$ (D: depth of the tree)) :
```python
class Solution:
    def removeLeafNodes(self, root: Optional[TreeNode], target: int) -> Optional[TreeNode]:
        need_remove = self.dfs(root, target)
        if need_remove:
            return None
        return root

    def dfs(self, node, target: int) -> bool:
        if node.left and self.dfs(node.left, target):
            node.left = None
        if node.right and self.dfs(node.right, target):
            node.right = None

        if node.left is None and node.right is None and node.val == target:
            return True
        return False
```
