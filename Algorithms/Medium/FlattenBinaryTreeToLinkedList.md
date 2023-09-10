![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 114. [Flatten Binary Tree To Linked List](https://leetcode.com/problems/flatten-binary-tree-to-linked-list)

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (Preorder, Space Complexity: $O(N)$) :
```python
class Solution:
    def flatten(self, root: Optional[TreeNode]) -> None:
        """
        Do not return anything, modify root in-place instead.
        """
        if root is None:
            return

        traverse = deque()
        self.preorder(root, traverse)

        traverse.popleft()
        node = root
        while traverse:
            node.left = None
            node.right = traverse.popleft()
            node = node.right

    def preorder(self, node, traverse):
        if node is None:
            return

        traverse.append(node)
        self.preorder(node.left, traverse)
        self.preorder(node.right, traverse)
```

Method 2 (Preorder, Space Complexity: $O(1)$) :
```python
class Solution:
    def flatten(self, root: Optional[TreeNode]) -> None:
        """
        Do not return anything, modify root in-place instead.
        """
        if root is None:
            return

        right = root.right
        root.right = root.left
        root.left = None

        self.flatten(root.right)
        self.flatten(right)

        while root and root.right:
            root = root.right
        root.right = right
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

Method 1 (Preorder, Space Complexity: $O(1)$) :
```php
class Solution {

    /**
     * @param TreeNode $root
     * @return NULL
     */
    function flatten(TreeNode|NULL $root) : void {
        if (is_null($root)) {
            return;
        }

        $right = $root->right;
        $root->right = $root->left;
        $root->left = NULL;
        $this->flatten($root->right);
        $this->flatten($right);

        $node = $root;
        while($node->right) {
            $node = $node->right;
        }
        $node->right = $right;
    }
}
```
