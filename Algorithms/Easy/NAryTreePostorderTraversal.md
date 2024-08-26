![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 590. [N-ary Tree Postorder Traversal](https://leetcode.com/problems/n-ary-tree-postorder-traversal)

### Solution :

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val=None, children=None):
        self.val = val
        self.children = children
"""
```

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(LOG(N))$ (N: number of the nodes in the tree)) :
```python
class Solution:
    def postorder(self, root: 'Node') -> List[int]:
        if not root:
            return []

        result = []
        if root.children:
            for child in root.children:
                result += self.postorder(child)

        result.append(root.val)
        return result
```
