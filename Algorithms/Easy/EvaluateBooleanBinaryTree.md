![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2331. [Evaluate Boolean Binary Tree](https://leetcode.com/problems/evaluate-boolean-binary-tree)

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (DFS, Time Complexity: $O(N)$, Space Complexity: $O(D)$ (D: depth of the tree, in worst case it is equal to `N`)) :
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
