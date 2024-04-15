![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
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

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (Recursive Traversal, Time Complexity: $O(N)$, Space Complexity: $O(D)$ (D: depth of the tree)) :
```python
class Solution:
    def sumNumbers(self, root: Optional[TreeNode]) -> int:
        if root is None:
            return 0
        return self.traverse(root, 0)

    def traverse(self, node: Optional[TreeNode], summarize: int) -> int:
        summarize = summarize*10 + node.val
        if node.left is None and node.right is None:
            return summarize

        result = 0
        if node.left:
            result += self.traverse(node.left, summarize)
        if node.right:
            result += self.traverse(node.right, summarize)

        return result
```

### Solution :

```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
```

Method 1 (Recursive Traversal, Time Complexity: $O(N)$, Space Complexity: $O(D)$ (D: depth of the tree)) :
```go
func sumNumbers(root *TreeNode) int {
    if root == nil {
        return 0
    }
    return traverse(root, 0)
}

func traverse(node *TreeNode, current int) int {
    var next int = current * 10 + node.Val
    if node.Left == nil && node.Right == nil {
        return next
    }

    var result int
    if node.Left != nil {
        result += traverse(node.Left, next)
    }
    if node.Right != nil {
        result += traverse(node.Right, next)
    }

    return result
}
```
