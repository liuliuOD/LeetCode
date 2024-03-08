![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1161. [Maximum Level Sum Of A Binary Tree](https://leetcode.com/problems/maximum-level-sum-of-a-binary-tree)

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
    def maxLevelSum(self, root: Optional[TreeNode]) -> int:
        level_sum = defaultdict(int)
        queue = deque([(1, root)])
        while queue:
            level, node = queue.popleft()
            if node is None:
                continue
            level_sum[level] += node.val
            queue.append((level + 1, node.left))
            queue.append((level + 1, node.right))

        temp_sum = -(10**5 + 1)
        result = 0
        for key, value in level_sum.items():
            if value > temp_sum:
                temp_sum = value
                result = key
        return result
```

Method 2 :
```python
class Solution:
    def maxLevelSum(self, root: Optional[TreeNode]) -> int:
        result = 0
        current_level = 1
        level_sum = -(10**5 + 1)
        stack = list([root])
        while stack:
            level_nodes = stack.copy()
            stack.clear()

            temp = 0
            while level_nodes:
                node = level_nodes.pop()
                temp += node.val
                if node.left:
                    stack.append(node.left)
                if node.right:
                    stack.append(node.right)

            if temp > level_sum:
                result = current_level
                level_sum = temp
            current_level += 1
        return result
```
