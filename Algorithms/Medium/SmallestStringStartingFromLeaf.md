![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 988. [Smallest String Starting From Leaf](https://leetcode.com/problems/smallest-string-starting-from-leaf)

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (Recursive DFS, Time Complexity: $O(N)$, Space Complexity: $O()$) :
```python
BASE: int = ord("a")
class Solution:
    def smallestFromLeaf(self, root: Optional[TreeNode]) -> str:
        self.result: str | None = None
        self.traverse(root, "")

        return self.result

    def traverse(self, node: Optional[TreeNode], string: str):
        string = chr(BASE+node.val) + string
        if node.left is None and node.right is None:
            if self.result is None:
                self.result = string
            else:
                self.result = min(self.result, string)
            return None

        if node.left:
            self.traverse(node.left, string)
        if node.right:
            self.traverse(node.right, string)
```
