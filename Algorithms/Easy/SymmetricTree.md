![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 101. [Symmetric Tree](https://leetcode.com/problems/symmetric-tree)

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (Traverse, Time Complexity: $O(N)$, Space Complexity: $O(H)$ (H: height of the tree)) :
```python
class Solution:
    def isSymmetric(self, root: Optional[TreeNode]) -> bool:
        self.result = True
        self.traverse(root.left, root.right)
        return self.result

    def traverse(self, node1, node2):
        if node1 is None and node2 is None:
            return
        if (node1 is None and node2 is not None) or (node1 is not None and node2 is None) or node1.val != node2.val:
            self.result = False
            return

        self.traverse(node1.left, node2.right)
        self.traverse(node1.right, node2.left)
```
