![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2096. [Step-By-Step Directions From A Binary Tree Node To Another](https://leetcode.com/problems/step-by-step-directions-from-a-binary-tree-node-to-another)

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (BFS, Time Complexity: $O(N)$, Space Complexity: $O(N^2)$ (N: number of the nodes in the tree)) :
```python
class Solution:
    def getDirections(self, root: Optional[TreeNode], startValue: int, destValue: int) -> str:
        direction_start, direction_dest = "", ""
        direction_start = self.bfs(root, startValue)
        direction_dest = self.bfs(root, destValue)

        result = ""
        while direction_start and direction_dest:
            if direction_start[0] != direction_dest[0]:
                break

            direction_start = direction_start[1:]
            direction_dest = direction_dest[1:]

        return result + "U"*len(direction_start) + direction_dest

    def bfs(self, root: Optional[TreeNode], value: int) -> str:
        queue = deque([(root, "")])
        while queue:
            node, direction = queue.popleft()
            if node.val == value:
                return direction

            if node.left:
                queue.append((node.left, direction+"L"))
            if node.right:
                queue.append((node.right, direction+"R"))
```
