![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1038. [Binary Search Tree To Greater Sum Tree](https://leetcode.com/problems/binary-search-tree-to-greater-sum-tree)

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

Method 1 (In-Order DFS, Time Complexity: $O(N)$ (N: number of the nodes in the tree), Space Complexity: $O(D)$ (D: depth of the tree)) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
type Custom = Option<Rc<RefCell<TreeNode>>>;
impl Solution {
    pub fn bst_to_gst(root: Custom) -> Custom {
        Self::traverse(root.clone(), 0);
        return root
    }

    fn traverse(mut node: Custom, mut sum_current: i32) -> i32 {
        match node {
            None => 0,
            Some(node) => {
                let mut inner = node.borrow_mut();
                if inner.left.is_none() && inner.right.is_none() {
                    inner.val += sum_current;
                    return inner.val
                }

                if inner.right.is_some() {
                    sum_current = Self::traverse(inner.right.clone(), sum_current);
                }

                inner.val += sum_current;
                sum_current = inner.val;

                if inner.left.is_some() {
                    sum_current = Self::traverse(inner.left.clone(), sum_current);
                }

                return sum_current
            }
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

Method 1 (In-Order DFS, Time Complexity: $O(N)$ (N: number of the nodes in the tree), Space Complexity: $O(D)$ (D: depth of the tree)) :
```python
class Solution:
    def bstToGst(self, root: TreeNode) -> TreeNode:
        self.sum_current = 0
        self.traverse(root)
        return root

    def traverse(self, node: TreeNode) -> None:
        if node.left is None and node.right is None:
            node.val += self.sum_current
            self.sum_current = node.val
            return None

        if node.right:
            self.traverse(node.right)

        node.val += self.sum_current
        self.sum_current = node.val

        if node.left:
            self.traverse(node.left)
```

Method 2 (In-Order DFS, Time Complexity: $O(N)$ (N: number of the nodes in the tree), Space Complexity: $O(D)$ (D: depth of the tree)) :
```python
class Solution:
    def bstToGst(self, root: TreeNode) -> TreeNode:
        self.traverse(root, 0)
        return root

    def traverse(self, node: TreeNode, sum_current: int) -> int:
        if node.left is None and node.right is None:
            node.val += sum_current
            return node.val

        if node.right:
            sum_current = self.traverse(node.right, sum_current)

        node.val += sum_current
        sum_current = node.val

        if node.left:
            sum_current = self.traverse(node.left, sum_current)

        return sum_current
```
