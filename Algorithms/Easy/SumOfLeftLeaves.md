![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 404. [Sum Of Left Leaves](https://leetcode.com/problems/sum-of-left-leaves)

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

Method 1 (Traverse, Time Complexity: $O(N)$ (N: amount of nodes), Space Complexity: $O(Log(N))$) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
impl Solution {
    pub fn sum_of_left_leaves(root: Option<Rc<RefCell<TreeNode>>>) -> i32 {
        return match root {
            None => 0,
            Some(root) => Self::find_left_leaves(true, &root.borrow().left) + Self::find_left_leaves(false, &root.borrow().right)
        }
    }

    fn find_left_leaves(is_left: bool, node: &Option<Rc<RefCell<TreeNode>>>) -> i32 {
        return match node {
            None => 0,
            Some(node) => {
                if node.borrow().left == None && node.borrow().right == None {
                    return match is_left {
                        true => node.borrow().val,
                        false => 0,
                    }
                }

                return Self::find_left_leaves(true, &node.borrow().left) + Self::find_left_leaves(false, &node.borrow().right)
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

Method 1 (Traverse, Time Complexity: $O(N)$ (N: amount of nodes), Space Complexity: $O(Log(N))$) :
```python
class Solution:
    def sumOfLeftLeaves(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0

        return self.findLeftLeaves(True, root.left) + self.findLeftLeaves(False, root.right)

    def findLeftLeaves(self, isLeft: bool, node: TreeNode) -> int:
        if not node:
            return 0

        if node.left is None and node.right is None:
            return node.val if isLeft else 0

        return self.findLeftLeaves(True, node.left) + self.findLeftLeaves(False, node.right)
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

Method 1 (Traverse, Time Complexity: $O(N)$ (N: amount of nodes), Space Complexity: $O(Log(N))$) :
```go
func sumOfLeftLeaves(root *TreeNode) int {
    return findLeftLeaves(true, root.Left) + findLeftLeaves(false, root.Right)
}

func findLeftLeaves(isLeft bool, node *TreeNode) int {
    if node == nil {
        return 0
    }

    if node.Left == nil && node.Right == nil {
        if isLeft {
            return node.Val
        }
        return 0
    }

    return findLeftLeaves(true, node.Left) + findLeftLeaves(false, node.Right)
}
```
