![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 124. [Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum)

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
class Solution:
    def maxPathSum(self, root: Optional[TreeNode]) -> int:
        self.result = float('-inf')
        self.dfs(root)
        return self.result

    def dfs(self, node) -> int:
        if node is None:
            return 0

        sum_left = max(0, self.dfs(node.left))
        sum_right = max(0, self.dfs(node.right))
        sum_current = node.val + sum_left + sum_right

        self.result = max(self.result, sum_current)

        return node.val + max(sum_left, sum_right)
```

### Solution :

```php
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     public $val = null;
 *     public $left = null;
 *     public $right = null;
 *     function __construct($val = 0, $left = null, $right = null) {
 *         $this->val = $val;
 *         $this->left = $left;
 *         $this->right = $right;
 *     }
 * }
 */
```

Method 1 (DFS) :
```php

class Solution {

    /**
     * @param TreeNode $root
     * @return Integer
     */
    function maxPathSum($root) {
        $this->result = PHP_INT_MIN;
        $this->dfs($root);
        return $this->result;
    }

    function dfs($node) : int {
        if (is_null($node)) {
            return 0;
        }

        $sumLeft = max(0, $this->dfs($node->left));
        $sumRight = max(0, $this->dfs($node->right));
        $sumCurrent = $node->val + $sumLeft + $sumRight;

        $this->result = max($this->result, $sumCurrent);

        return $node->val + max($sumLeft, $sumRight);
    }
}
```
