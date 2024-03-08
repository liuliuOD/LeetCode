![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 530. [Minimum Absolute Difference In BST](https://leetcode.com/problems/minimum-absolute-difference-in-bst)

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (Transfer BST to List) :
```python
INT_MAX = 10**5
class Solution:
    def getMinimumDifference(self, root: Optional[TreeNode]) -> int:
        ordered = list()
        traverse_queue = list([root])
        while len(traverse_queue):
            item = traverse_queue.pop()
            if item is None:
                continue
            ordered.append(item.val)
            traverse_queue.append(item.left)
            traverse_queue.append(item.right)
        
        ordered.sort()
        result = INT_MAX
        for index in range(len(ordered)-1):
            result = min(result, abs(ordered[index] - ordered[index+1]))
        return result
```

Method 2 (Use Inorder Traverse to get ordered list in BST) :
```python
INT_MAX = 10**5
class Solution:
    def getMinimumDifference(self, root: Optional[TreeNode]) -> int:
        self.ordered = list()
        self.inorder(root)

        result = INT_MAX
        for index in range(len(self.ordered) - 1):
            result = min(result, self.ordered[index+1] - self.ordered[index])
        return result

    def inorder(self, node: Optional[TreeNode]):
        if node is None:
            return
        self.inorder(node.left)
        self.ordered.append(node.val)
        self.inorder(node.right)
```

Method 3 :
```python
INT_MAX = 10**5
class Solution:
    def getMinimumDifference(self, root: Optional[TreeNode]) -> int:
        self.result = INT_MAX
        self.previous = None
        self.inorder(root)

        return self.result

    def inorder(self, node: Optional[TreeNode]):
        if node is None:
            return

        self.inorder(node.left)

        if self.previous is not None:
            self.result = min(self.result, node.val - self.previous)
        self.previous = node.val

        self.inorder(node.right)
```
