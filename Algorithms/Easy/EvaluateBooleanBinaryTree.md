![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2331. [Evaluate Boolean Binary Tree](https://leetcode.com/problems/evaluate-boolean-binary-tree)

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

Method 1 (Recursive DFS, Time Complexity: $O(N)$, Space Complexity: $O(D)$ (D: depth of the tree, in worst case it is equal to `N`)) :
```rust
use std::rc::Rc;
use std::cell::{Ref, RefCell};
impl Solution {
    pub fn evaluate_tree(root: Option<Rc<RefCell<TreeNode>>>) -> bool {
        let current: Ref<'_, TreeNode> = root.as_ref().unwrap().borrow();
        if current.left.is_none() && current.right.is_none() {
            return current.val == 1
        }

        let left: bool = Self::evaluate_tree(current.left.clone());
        let right: bool = Self::evaluate_tree(current.right.clone());
        return match current.val {
            2 => left || right,
            3 => left && right,
            _ => false
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

Method 1 (Recursive DFS, Time Complexity: $O(N)$, Space Complexity: $O(D)$ (D: depth of the tree, in worst case it is equal to `N`)) :
```python
class Solution:
    def evaluateTree(self, root: Optional[TreeNode]) -> bool:
        current = root.val
        if root.left is None and root.right is None:
            # Option 1
            return bool(current)
            """
            # Option 2

            return current != 0
            """

        left = self.evaluateTree(root.left)
        right = self.evaluateTree(root.right)

        return left or right if current == 2 else left and right
```

Method 2 (Iterative DFS + Stack, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def evaluateTree(self, root: Optional[TreeNode]) -> bool:
        result = defaultdict(None)
        stack = [root]
        while stack:
            node = stack[-1]
            if node.left is None and node.right is None:
                stack.pop()

                result[node] = (node.val == 1)
                continue

            if node.left not in result or node.right not in result:
                if node.left:
                    stack.append(node.left)
                if node.right:
                    stack.append(node.right)
            else:
                stack.pop()

                if node.val == 2:
                    result[node] = result[node.left] or result[node.right]
                elif node.val == 3:
                    result[node] = result[node.left] and result[node.right]

        return result[root]
```
