![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1530. [Number Of Good Leaf Nodes Pairs](https://leetcode.com/problems/number-of-good-leaf-nodes-pairs)

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (DFS) :
```python

DEPTH = 12
class Solution:
    def countPairs(self, root: TreeNode, distance: int) -> int:
        return self.traverse(root, distance)[-1]

    def traverse(self, node: TreeNode | None, distance: int) -> list[int]:
        if node is None:
            return [0] * DEPTH
        elif node.left is None and node.right is None:
            return [1] + [0]*(DEPTH - 1)

        """
        # index 0 ~ 10: numbers of the nodes in current subtree
        # index 11: the amount of the nodes that are good leaf nodes
        """
        good_leaf_nodes = [0] * DEPTH
        good_leaf_nodes_subtree_left = self.traverse(node.left, distance)
        good_leaf_nodes_subtree_right = self.traverse(node.right, distance)

        good_leaf_nodes[-1] = good_leaf_nodes_subtree_left[-1] + good_leaf_nodes_subtree_right[-1]
        for index in range(DEPTH-2):
            good_leaf_nodes[index+1] = good_leaf_nodes_subtree_left[index] + good_leaf_nodes_subtree_right[index]

        for distance_left in range(distance):
            for distance_right in range(distance):
                if distance_left + distance_right + 2 > distance:
                    break

                good_leaf_nodes[-1] += good_leaf_nodes_subtree_left[distance_left] * good_leaf_nodes_subtree_right[distance_right]

        return good_leaf_nodes
```
