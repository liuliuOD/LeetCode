![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 513. [Find Bottom Left Tree Value](https://leetcode.com/problems/find-bottom-left-tree-value)

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (BFS) :
```python
class Solution:
    def findBottomLeftValue(self, root: Optional[TreeNode]) -> int:
        if root is None:
            return None

        result = [0, root.val]
        queue = deque([(0, root)])
        while queue:
            depth, node = queue.popleft()
            if depth > result[0]:
                result = [depth, node.val]

            if node.left:
                queue.append((depth+1, node.left))
            if node.right:
                queue.append((depth+1, node.right))

        return result[1]
```
