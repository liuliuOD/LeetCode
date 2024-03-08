![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 606. [Construct String From Binary Tree](https://leetcode.com/problems/construct-string-from-binary-tree)

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (Recursive DFS, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def tree2str(self, root: Optional[TreeNode]) -> str:
        if root is None:
            return ""

        result = f"{root.val}"
        if root.left is None and root.right is None:
            return result

        left = self.tree2str(root.left)
        right = self.tree2str(root.right)
        result = f"{result}({left})"
        if right != "":
            result = f"{result}({right})"

        return result
```
