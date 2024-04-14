![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 404. [Sum Of Left Leaves](https://leetcode.com/problems/sum-of-left-leaves)

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (Traverse, Time Complexity: $O(N)$ (N: amount of nodes), Space Complexity: $O(Log(N))$) :
```python
class Solution:
    def sumOfLeftLeaves(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0

        return self.findLeftLeaves(True, root.left) + self.findLeftLeaves(False, root.right)

    def findLeftLeaves(self, isLeft: bool, node: TreeNode) -> int:
        if not node:
            return 0

        if node.left is None and node.right is None:
            return node.val if isLeft else 0

        return self.findLeftLeaves(True, node.left) + self.findLeftLeaves(False, node.right)
```

### Solution :

```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
```

Method 1 (Traverse, Time Complexity: $O(N)$ (N: amount of nodes), Space Complexity: $O(Log(N))$) :
```go
func sumOfLeftLeaves(root *TreeNode) int {
    return findLeftLeaves(true, root.Left) + findLeftLeaves(false, root.Right)
}

func findLeftLeaves(isLeft bool, node *TreeNode) int {
    if node == nil {
        return 0
    }

    if node.Left == nil && node.Right == nil {
        if isLeft {
            return node.Val
        }
        return 0
    }

    return findLeftLeaves(true, node.Left) + findLeftLeaves(false, node.Right)
}
```
