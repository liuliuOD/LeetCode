![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 543. [Diameter Of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree)

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (DFS, Time Complexity: $O(N)$ (N: amount of nodes), Space Complexity: $O(M+N)$ (M: depth of tree)) :
```python
class Solution:
    def diameterOfBinaryTree(self, root: Optional[TreeNode]) -> int:
        if root is None:
            return 1

        mapping = defaultdict(int)
        mapping[id(root)] = self.getDepth(0, root.left, mapping) + self.getDepth(0, root.right, mapping)
        return max(mapping.values())

    def getDepth(self, depth: int, node: Optional[TreeNode], mapping: Dict[TreeNode, int]) -> int:
        if node is None:
            return depth

        depth_left = self.getDepth(depth+1, node.left, mapping)
        depth_right = self.getDepth(depth+1, node.right, mapping)
        mapping[id(node)] = depth_left + depth_right - (depth+1) * 2
        return max(depth_left, depth_right)
```
