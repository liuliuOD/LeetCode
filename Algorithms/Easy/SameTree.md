![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 100. [Same Tree](https://leetcode.com/problems/same-tree)

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (Recursive) :
```python
class Solution:
    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        if p is None and q is None:
            return True

        if (p is None and q) or (p and q is None):
            return False

        if p.val != q.val:
            return False

        if not self.isSameTree(p.left, q.left):
            return False

        if not self.isSameTree(p.right, q.right):
            return False

        return True
```

Method 2 (Recursive, Time Complexity: $O(MIN(M, N))$ (M: `amount` of p nodes, N: `amount` of q nodes), Space Complexity: $O(MIN(Hm, Hn))$) (Hm: `height` of tree p, Hn: `height` of tree q) :
```python
class Solution:
    def isSameTree(self, p: Optional[TreeNode], q: Optional[TreeNode]) -> bool:
        if p is None and q is None:
            return True

        if p and q and p.val == q.val:
            return self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)

        return False
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

Method 1 (Recursive) :
```php
class Solution {

    /**
     * @param TreeNode $p
     * @param TreeNode $q
     * @return Boolean
     */
    function isSameTree($p, $q) {
        if (is_null($p) && is_null($q)) {
            return true;
        } else if (($p && is_null($q)) || (is_null($p) && $q)) {
            return false;
        }

        if ($p->val != $q->val) {
            return false;
        }

        if (!$this->isSameTree($p->left, $q->left)) {
            return false;
        }
        if (!$this->isSameTree($p->right, $q->right)) {
            return false;
        }

        return true;
    }
}
```

Method 2 (Recursive) :
```php
class Solution {

    /**
     * @param TreeNode $p
     * @param TreeNode $q
     * @return Boolean
     */
    function isSameTree($p, $q) {
        if (is_null($p) || is_null($q)) {
            return $p == $q;
        }

        return $p->val == $q->val
            && $this->isSameTree($p->left, $q->left)
            && $this->isSameTree($p->right, $q->right);
    }
}
```
