![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 938. [Range Sum Of BST](https://leetcode.com/problems/range-sum-of-bst)

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

Method 1 (Recursion, Time Complexity: $O(N)$, Space Complexity: $O(D)$ (D: depth of binary search tree)) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
impl Solution {
    pub fn range_sum_bst(root: Option<Rc<RefCell<TreeNode>>>, low: i32, high: i32) -> i32 {
        return Self::traverse(&root, low, high)
    }

    fn traverse(node: &Option<Rc<RefCell<TreeNode>>>, low: i32, high: i32) -> i32 {
        return match node {
            None => 0,
            Some(node) => {
                let mut result: i32 = 0;
                let val: i32 = node.borrow().val;
                /* Option 1*/
                if val < low {
                    result += Self::traverse(&node.borrow().right, low, high);
                }
                else if high < val {
                    result += Self::traverse(&node.borrow().left, low, high);
                }
                else if low <= val && val <= high {
                    result += val + Self::traverse(&node.borrow().left, low, high) + Self::traverse(&node.borrow().right, low, high);
                }
                /*
                // Option 2

                if low <= val && val <= high {
                    result += val;
                }

                if low <= val {
                    result += Self::traverse(&node.borrow().left, low, high);
                }
                if val <= high {
                    result += Self::traverse(&node.borrow().right, low, high);
                }
                */

                return result
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

Method 1 (Recursion, Time Complexity: $O(N)$, Space Complexity: $O(D)$ (D: depth of binary search tree)) :
```python
class Solution:
    def rangeSumBST(self, root: Optional[TreeNode], low: int, high: int) -> int:
        if root is None:
            return 0

        # Option 1
        if root.val < low:
            return self.rangeSumBST(root.right, low, high)
        if root.val > high:
            return self.rangeSumBST(root.left, low, high)

        return root.val + self.rangeSumBST(root.left, low, high) + self.rangeSumBST(root.right, low, high)
        """
        # Option 2

        left = self.rangeSumBST(root.right, low, high)
        right = self.rangeSumBST(root.left, low, high)
        if root.val < low:
            return left
        if root.val > high:
            return right

        return root.val + left + right
        """
```
