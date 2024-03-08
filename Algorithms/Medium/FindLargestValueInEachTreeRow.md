![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 515. [Find Largest Value In Each Tree Row](https://leetcode.com/problems/find-largest-value-in-each-tree-row)

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
    def largestValues(self, root: Optional[TreeNode]) -> List[int]:
        result = []
        # push `root` into queue when root exists
        queue = deque([root] if root else [])
        while queue:
            amount = len(queue)
            temp = -inf
            for _ in range(amount):
                node = queue.popleft()
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)

                temp = max(temp, node.val)

            result.append(temp)

        return result
```

Method 2 (BFS + Binary Heap) :
```python
class Solution:
    def largestValues(self, root: Optional[TreeNode]) -> List[int]:
        result = []
        queue = deque([root] if root else [])
        while queue:
            amount = len(queue)
            heap = []
            for _ in range(amount):
                node = queue.popleft()
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)

                heapq.heappush(heap, -node.val)

            result.append(-heapq.heappop(heap))

        return result
```

Method 3 (DFS) :
```python
class Solution:
    def largestValues(self, root: Optional[TreeNode]) -> List[int]:
        result = defaultdict(lambda: -inf)
        self.dfs(root, 0, result)
        return result.values()

    def dfs(self, node, depth, result):
        if node is None:
            return

        result[depth] = max(result[depth], node.val)
        self.dfs(node.left, depth+1, result)
        self.dfs(node.right, depth+1, result)
```
