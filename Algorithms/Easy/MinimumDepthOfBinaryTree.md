![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 111. [Minimum Depth Of Binary Tree](https://leetcode.com/problems/minimum-depth-of-binary-tree)

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
    def minDepth(self, root: Optional[TreeNode]) -> int:
        return self.traverse(root, 1)

    def traverse(self, node: TreeNode, depth: int) -> Optional[int]:
        if node is None:
            return 0
        
        if node.left is None and node.right is None:
            return depth
        
        depth_next = depth + 1
        left = right = float('inf')
        if node.left:
            left = self.traverse(node.left, depth_next)
        if node.right:
            right = self.traverse(node.right, depth_next)
        return min(left, right)
```

Method 2 (BFS) :
```python
class Solution:
    def minDepth(self, root: Optional[TreeNode]) -> int:
        queue = deque([(root, 1)])
        while queue:
            node, depth = queue.popleft()

            # valid if root is None
            if node is None:
                return 0
            
            if node.left is None and node.right is None:
                return depth
            
            if node.left:
                queue.append((node.left, depth + 1))
            if node.right:
                queue.append((node.right, depth + 1))
```
