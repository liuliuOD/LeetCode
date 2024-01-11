![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1026. [Maximum Difference Between Node And Ancestor](https://leetcode.com/problems/maximum-difference-between-node-and-ancestor)

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
    def maxAncestorDiff(self, root: Optional[TreeNode]) -> int:
        result = 0
        queue = deque([(root, root.val, root.val)])
        while queue:
            node, minimum, maximum = queue.popleft()

            if node.left:
                node_next = node.left
                minimum_next = min(minimum, node_next.val)
                maximum_next = max(maximum, node_next.val)
                result = max(result, maximum_next - minimum_next)
                queue.append((node_next, minimum_next, maximum_next))
            if node.right:
                node_next = node.right
                minimum_next = min(minimum, node_next.val)
                maximum_next = max(maximum, node_next.val)
                result = max(result, maximum_next - minimum_next)
                queue.append((node_next, minimum_next, maximum_next))

        return result
```

Method 2 (DFS, Time Complexity: $O(N)$, Space Complexity: $O(D)$ (D: depth of the tree)) :
```python
class Solution:
    def maxAncestorDiff(self, root: Optional[TreeNode]) -> int:
        return self.dfs(root, root.val, root.val)

    def dfs(self, node: Optional[TreeNode], minimum: int, maximum: int) -> int:
        if node is None:
            return 0

        if node.left is None and node.left == node.right:
            return maximum - minimum

        result = 0
        if node.left:
            result = max(result, self.dfs(node.left, min(minimum, node.left.val), max(maximum, node.left.val)))
        if node.right:
            result = max(result, self.dfs(node.right, min(minimum, node.right.val), max(maximum, node.right.val)))

        return result
```
