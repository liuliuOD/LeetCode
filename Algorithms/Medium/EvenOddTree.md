![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1609. [Even Odd Tree](https://leetcode.com/problems/even-odd-tree)

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
    def isEvenOddTree(self, root: Optional[TreeNode]) -> bool:
        previous = (0, 0)
        queue = deque([(0, root)])
        while queue:
            index, node = queue.popleft()
            if previous[0] != index:
                if previous[0] % 2 == 0 and previous[1] % 2 == 0:
                    return False
                elif previous[0] % 2 == 1 and previous[1] % 2 == 1:
                    return False

                previous = (index, node.val)
            elif index % 2 == 0:
                if previous[1] >= node.val:
                    return False

                previous = (previous[0], node.val)
            elif index % 2 == 1:
                if previous[1] <= node.val:
                    return False

                previous = (previous[0], node.val)

            if node.left:
                queue.append((index+1, node.left))
            if node.right:
                queue.append((index+1, node.right))

        if previous[0] % 2 == 0:
            return previous[1] % 2 == 1

        return previous[1] % 2 == 0
```
