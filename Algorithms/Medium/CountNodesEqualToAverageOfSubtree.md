![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2265. [Count Nodes Equal To Average Of Subtree](https://leetcode.com/problems/count-nodes-equal-to-average-of-subtree)

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (Recursive Post-Order DFS + Memoization, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def averageOfSubtree(self, root: Optional[TreeNode]) -> int:
        # node: [sum of node.val, amount of nodes]
        memoization: Dict[TreeNode, List[int]] = {}
        self.dfs(root, memoization)

        return sum([node.val == (summation//amount) for node, [summation, amount] in memoization.items()])

    def dfs(self, node: Optional[TreeNode], memoization: Dict[TreeNode, List[int]]) -> List[int]:
        if not node:
            return [0, 0]

        if node in memoization:
            return memoization[node]

        result = [sum(items) for items in zip([node.val, 1], self.dfs(node.left, memoization), self.dfs(node.right, memoization))]

        memoization[node] = result
        return result
```

Method 2 (Recursive Post-Order DFS, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (because the stack space used in recursion)) :
```python
class Solution:
    def averageOfSubtree(self, root: Optional[TreeNode]) -> int:
        self.result = 0
        self.dfs(root)

        return self.result

    def dfs(self, node: Optional[TreeNode]) -> List[int]:
        if not node:
            return [0, 0]

        left = self.dfs(node.left)
        right = self.dfs(node.right)
        summation = left[0] + right[0] + node.val
        amount = left[1] + right[1] + 1
        self.result += node.val == (summation//amount)

        return [summation, amount]
```

Method 3 (Iterative Post-Order DFS, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def averageOfSubtree(self, root: Optional[TreeNode]) -> int:
        result = 0
        stack = [(root, False)]
        while stack:
            node, visited = stack.pop()
            if not node:
                continue

            if visited:
                summation = node.val
                amount = 1
                if node.left:
                    summation += node.left.val[0]
                    amount += node.left.val[1]
                if node.right:
                    summation += node.right.val[0]
                    amount += node.right.val[1]

                if node.val == (summation//amount):
                    result += 1

                """
                Modify node value in-line can reduce memory usage
                """
                node.val = [summation, amount]
                continue

            stack.append((node, True))
            stack.append((node.left, False))
            stack.append((node.right, False))

        return result
```
