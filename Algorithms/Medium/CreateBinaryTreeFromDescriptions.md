![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2196. [Create Binary Tree From Descriptions](https://leetcode.com/problems/pseudo-palindromic-paths-in-a-binary-tree)

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: numbers of the elements in `descriptions`)) :
```python
class Solution:
    def createBinaryTree(self, descriptions: List[List[int]]) -> Optional[TreeNode]:
        candidates: dict[TreeNode] = dict()
        indegree: dict[int] = defaultdict(int)
        for parent, value, is_left in descriptions:
            indegree[value] += 1
            if parent not in candidates:
                candidates[parent] = TreeNode(val=parent)

            if value not in candidates:
                candidates[value] = TreeNode(val=value)

            if is_left:
                candidates[parent].left = candidates[value]
            else:
                candidates[parent].right = candidates[value]

        for node in candidates.keys():
            if node in indegree or indegree[node] > 0:
                continue

            return candidates[node]
        return None
```
