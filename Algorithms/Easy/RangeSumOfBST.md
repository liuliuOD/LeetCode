![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 938. [Range Sum Of BST](https://leetcode.com/problems/range-sum-of-bst)

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
