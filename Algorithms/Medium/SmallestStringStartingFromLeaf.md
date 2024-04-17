![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 988. [Smallest String Starting From Leaf](https://leetcode.com/problems/smallest-string-starting-from-leaf)

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (Recursive DFS, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
BASE: int = ord("a")
class Solution:
    def smallestFromLeaf(self, root: Optional[TreeNode]) -> str:
        self.result: str | None = None
        self.traverse(root, "")

        return self.result

    def traverse(self, node: Optional[TreeNode], string: str):
        string = chr(BASE+node.val) + string
        if node.left is None and node.right is None:
            # Option 1
            if self.result is None:
                self.result = string
            else:
                self.result = min(self.result, string)
            """
            # Option 2

            if self.result is None or self.result > string:
                self.result = string
            """
            return None

        if node.left:
            self.traverse(node.left, string)
        if node.right:
            self.traverse(node.right, string)
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

Method 1 (Recursive DFS, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```go
const BASE int = int('a')
var result string
func smallestFromLeaf(root *TreeNode) string {
    /* Use `defer` to rollback the value of `result` to prevent global assignment */
    defer func () {
        result = ""
    }()
    traverse(root, "")
    return result
}

func traverse(node *TreeNode, current string) {
    if node == nil {
        return
    }

    current = string(node.Val + BASE) + current
    if node.Left == nil && node.Right == nil {
        if result == "" || result > current {
            result = current
        }

        return
    }

    traverse(node.Left, current)
    traverse(node.Right, current)
}
```
