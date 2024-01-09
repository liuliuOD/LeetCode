![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 872. [Leaf-Similar Trees](https://leetcode.com/problems/leaf-similar-trees)

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (Recursion, Time Complexity: $O(N1+N2)$ (N1: amount of nodes in `root1`, N2: amount of nodes in `root2`), Space Complexity: $O(N1+N2)$) :
```python
class Solution:
    def leafSimilar(self, root1: Optional[TreeNode], root2: Optional[TreeNode]) -> bool:
        return self.traverse(root1) == self.traverse(root2)

    def traverse(self, node: Optional[TreeNode]) -> List[int]:
        if node is None:
            return []

        if node.left == node.right and node.left is None:
            return [node.val]

        return self.traverse(node.left) + self.traverse(node.right)
```

Method 2 :
```python
class Solution:
    def leafSimilar(self, root1: Optional[TreeNode], root2: Optional[TreeNode]) -> bool:
        # Option 1
        return list(self.traverse(root1)) == list(self.traverse(root2))
        """
        # Option 2

        return all([node1 == node2 for node1, node2 in zip_longest(self.traverse(root1), self.traverse(root2))])
        """
        """
        # Option 3

        for node1, node2 in zip_longest(self.traverse(root1), self.traverse(root2)):
            if node1 != node2:
                return False

        return True
        """

    def traverse(self, node: Optional[TreeNode]) -> Optional[int]:
        if node is None:
            return

        if node.left == node.right and node.left is None:
            yield node.val

        yield from self.traverse(node.left)
        yield from self.traverse(node.right)
```
