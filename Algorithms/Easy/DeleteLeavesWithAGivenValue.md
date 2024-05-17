![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1325. [Delete Leaves With A Given Value](https://leetcode.com/problems/delete-leaves-with-a-given-value)

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
