![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1457. [Pseudo-Palindromic Paths In A Binary Tree](https://leetcode.com/problems/pseudo-palindromic-paths-in-a-binary-tree)

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (Backtracking) :
```python
class Solution:
    def pseudoPalindromicPaths (self, root: Optional[TreeNode]) -> int:
        if root is None:
            return 0

        self.path = defaultdict(int)
        self.result = 0
        self.backtracking(root)
        return self.result

    def backtracking(self, root: Optional[TreeNode]):
        self.path[root.val] += 1

        if root.left is None and root.right is None:
            if self.hasPalindrome():
                self.result += 1

            self.path[root.val] -= 1
            return None

        if root.left:
            self.backtracking(root.left)
        if root.right:
            self.backtracking(root.right)

        self.path[root.val] -= 1

    def hasPalindrome(self) -> bool:
        odd = 0
        total = 0
        for amount in self.path.values():
            total += amount
            if amount % 2 == 1:
                odd += 1

        if odd > 1 or (odd == 1 and total % 2 == 0):
            return False

        return True
```
