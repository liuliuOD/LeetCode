![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1038. [Binary Search Tree To Greater Sum Tree](https://leetcode.com/problems/binary-search-tree-to-greater-sum-tree)

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (In-Order DFS, Time Complexity: $O(N)$ (N: number of the nodes in the tree), Space Complexity: $O(D)$ (D: depth of the tree)) :
```python
class Solution:
    def bstToGst(self, root: TreeNode) -> TreeNode:
        self.sum_current = 0
        self.traverse(root)
        return root

    def traverse(self, node: TreeNode) -> None:
        if node.left is None and node.right is None:
            node.val += self.sum_current
            self.sum_current = node.val
            return None

        if node.right:
            self.traverse(node.right)

        node.val += self.sum_current
        self.sum_current = node.val

        if node.left:
            self.traverse(node.left)
```

Method 2 (In-Order DFS, Time Complexity: $O(N)$ (N: number of the nodes in the tree), Space Complexity: $O(D)$ (D: depth of the tree)) :
```python
class Solution:
    def bstToGst(self, root: TreeNode) -> TreeNode:
        self.traverse(root, 0)
        return root

    def traverse(self, node: TreeNode, sum_current: int) -> int:
        if node.left is None and node.right is None:
            node.val += sum_current
            return node.val

        if node.right:
            sum_current = self.traverse(node.right, sum_current)

        node.val += sum_current
        sum_current = node.val

        if node.left:
            sum_current = self.traverse(node.left, sum_current)

        return sum_current
```
