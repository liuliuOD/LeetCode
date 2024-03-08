![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 863. [All Nodes Distance K In Binary Tree](https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree)

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None
```

Method 1 (DFS + Store Path) :
```python
class Solution:
    def distanceK(self, root: TreeNode, target: TreeNode, k: int) -> List[int]:
        path = []
        self.getTraversePath(path, root, target)

        n = len(path)
        traversed_nodes = set()
        result = []
        for index_path in reversed(range(n)):
            self.getDistanceKNode(result, path[index_path], k - (n - index_path - 1), traversed_nodes)

        return result

    def getTraversePath(self, path: List[TreeNode], current: TreeNode, target: TreeNode) -> bool:
        if current is None:
            return False
        
        path.append(current)
        if current == target:
            return True
        
        if self.getTraversePath(path, current.left, target) or self.getTraversePath(path, current.right, target):
            return True
        
        path.pop()

        return False
        
    def getDistanceKNode(self, result: List[int], node: TreeNode, k: int, traversed_nodes: Set[TreeNode]) -> Optional:
        # to prevent duplicate by traversed nodes and skip None
        if node in traversed_nodes or node is None:
            return None
        traversed_nodes.add(node)

        if k == 0:
            return result.append(node.val)
        elif k < 0:
            return None
        
        self.getDistanceKNode(result, node.left, k-1, traversed_nodes)
        self.getDistanceKNode(result, node.right, k-1, traversed_nodes)
```
