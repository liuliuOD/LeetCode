![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 623. [Add One Row To Tree](https://leetcode.com/problems/add-one-row-to-tree)

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (BFS, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def addOneRow(self, root: Optional[TreeNode], val: int, depth: int) -> Optional[TreeNode]:
        if depth == 1:
            return TreeNode(val=val, left=root)

        queue = deque([(root, 1)])
        while queue:
            node, depth_current = queue.popleft()
            if node is None:
                continue
            if depth_current >= depth:
                break

            queue.append((node.left, depth_current+1))
            queue.append((node.right, depth_current+1))

            if depth_current == depth-1:
                node.left = TreeNode(val=val, left=node.left)
                node.right = TreeNode(val=val, right=node.right)

        return root
```
