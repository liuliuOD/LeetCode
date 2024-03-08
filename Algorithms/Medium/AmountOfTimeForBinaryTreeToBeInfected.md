![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2385. [Amount Of Time For Binary Tree To Be Infected](https://leetcode.com/problems/amount-of-time-for-binary-tree-to-be-infected)

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (BFS + Adjacency List, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def amountOfTime(self, root: Optional[TreeNode], start: int) -> int:
        mapping = defaultdict(list)
        queue = deque([root])
        while queue:
            node = queue.popleft()
            if node is None:
                continue

            if node.left:
                mapping[node.val].append(node.left.val)
                mapping[node.left.val].append(node.val)
                queue.append(node.left)
            if node.right:
                mapping[node.val].append(node.right.val)
                mapping[node.right.val].append(node.val)
                queue.append(node.right)

        result = 0
        visited = set([start])
        queue = deque([(node_next, 1) for node_next in mapping[start]])
        while queue:
            node, minutes = queue.popleft()
            if node in visited:
                continue
            visited.add(node)

            result = max(result, minutes)
            for node_next in mapping[node]:
                queue.append((node_next, minutes+1))

        return result
```
