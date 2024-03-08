![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 133. [Clone Graph](https://leetcode.com/problems/clone-graph)

### Solution :

```python
"""
# Definition for a Node.
class Node:
    def __init__(self, val = 0, neighbors = None):
        self.val = val
        self.neighbors = neighbors if neighbors is not None else []
"""
```

Method 1 (Hash Map) :
```python
from typing import Optional
class Solution:
    def cloneGraph(self, node: Optional['Node']) -> Optional['Node']:
        if node is None:
            return node

        mapping = {}
        node_new = None
        stack = [node]
        while stack:
            temp = stack.pop()

            if temp.val in mapping:
                continue
            if temp.val not in mapping:
                mapping[temp.val] = Node(val=temp.val)
                if node_new is None:
                    node_new = mapping[temp.val]

            for neighbor in temp.neighbors:
                stack.append(neighbor)

        stack = [node]
        visited = set()
        while stack:
            temp = stack.pop()
            if temp.val in visited:
                continue
            visited.add(temp.val)

            for neighbor in temp.neighbors:
                stack.append(neighbor)
                mapping[temp.val].neighbors.append(mapping[neighbor.val])

        return node_new
```

Method 2 (Hash Map) :
```python
from typing import Optional
class Solution:
    def cloneGraph(self, node: Optional['Node']) -> Optional['Node']:
        if node is None:
            return node

        mapping = {node.val: Node(node.val)}
        stack = [node]
        visited = set()
        while stack:
            temp = stack.pop()
            key = temp.val
            if key in visited:
                continue
            visited.add(key)

            for neighbor in temp.neighbors:
                key_neighbor = neighbor.val
                if key_neighbor not in mapping:
                    mapping[key_neighbor] = Node(key_neighbor)

                mapping[key].neighbors.append(mapping[key_neighbor])
                stack.append(neighbor)

        return mapping[node.val]
```
