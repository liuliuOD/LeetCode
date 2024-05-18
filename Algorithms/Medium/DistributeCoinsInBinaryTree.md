![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 979. [Distribute Coins In Binary Tree](https://leetcode.com/problems/distribute-coins-in-binary-tree)

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
