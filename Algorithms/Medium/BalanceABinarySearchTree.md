![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1382. [Balance A Binary Search Tree](https://leetcode.com/problems/balance-a-binary-search-tree)

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (Recursively DFS + Array, Time Complexity: $O(N)$ (N: number of the nodes in the tree), Space Complexity: $O(D)$ (D: depth of the tree)) :
```python
class Solution:
    def balanceBST(self, root: TreeNode) -> TreeNode:
        ordered = []
        self.traverse(root, ordered)
        
        return self.build_tree(ordered)

    def traverse(self, node: TreeNode, ordered: list[int]) -> None:
        if node.left is None and node.right is None:
            ordered.append(node.val)
            return

        if node.left:
            self.traverse(node.left, ordered)

        ordered.append(node.val)

        if node.right:
            self.traverse(node.right, ordered)

    def build_tree(self, ordered: list[int]) -> TreeNode | None:
        if not ordered:
            return None

        # Option 1
        if len(ordered) == 1:
            return TreeNode(val=ordered[0])
        """
        # Option 2
        """

        index_middle = len(ordered) // 2
        return TreeNode(val=ordered[index_middle], left=self.build_tree(ordered[:index_middle]), right=self.build_tree(ordered[index_middle+1:]))
```
