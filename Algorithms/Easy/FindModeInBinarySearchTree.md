![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 501. [Find Mode In Binary Search Tree](https://leetcode.com/problems/find-mode-in-binary-search-tree)

### Follow Up:

- Could you do that without using any extra space? (Assume that the implicit stack space incurred due to recursion does not count).

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (Recursive DFS + Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findMode(self, root: Optional[TreeNode]) -> List[int]:
        mapping = defaultdict(int)
        self.traverse(root, mapping)

        maximum = max(mapping.values())
        return [key for key, value in mapping.items() if value == maximum]

    def traverse(self, node: Optional[TreeNode], mapping: Dict[int, int]):
        if not node:
            return

        mapping[node.val] += 1
        self.traverse(node.left, mapping)
        self.traverse(node.right, mapping)
```

Method 2 (Iterative DFS + Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findMode(self, root: Optional[TreeNode]) -> List[int]:
        maximum = 0
        mapping = defaultdict(int)
        stack = [root]
        while stack:
            node = stack.pop()
            if not node:
                continue

            mapping[node.val] += 1
            maximum = max(maximum, mapping[node.val])
            stack.append(node.right)
            stack.append(node.left)

        return [key for key, value in mapping.items() if value == maximum]
```

Method 3 (BFS + Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findMode(self, root: Optional[TreeNode]) -> List[int]:
        maximum = 0
        mapping = defaultdict(int)
        queue = deque([root])
        while queue:
            node = queue.popleft()
            if not node:
                continue

            mapping[node.val] += 1
            maximum = max(maximum, mapping[node.val])
            queue.append(node.left)
            queue.append(node.right)

        return [key for key, value in mapping.items() if value == maximum]
```

Method 4 (In-Order DFS + List, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findMode(self, root: Optional[TreeNode]) -> List[int]:
        """
        Hint: in most conditions, list use less memory space and execution time than hash map
        """
        nodes_sorted = []
        self.dfs(root, nodes_sorted)

        maximum = 0
        amount_current = 0
        current = nodes_sorted[0]
        result = [nodes_sorted[0]]
        for node in nodes_sorted:
            if node == current:
                amount_current += 1
            else:
                current = node
                amount_current = 1

            if maximum == amount_current:
                result.append(node)
            elif maximum < amount_current:
                maximum = amount_current
                result = [node]

        return result

    def dfs(self, node: Optional[TreeNode], nodes_sorted: List[int]):
        if not node:
            return

        self.dfs(node.left, nodes_sorted)
        nodes_sorted.append(node.val)
        self.dfs(node.right, nodes_sorted)
```
