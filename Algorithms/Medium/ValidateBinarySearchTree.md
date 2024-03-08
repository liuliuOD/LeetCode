![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 98. [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree)

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (Recursive In-Order DFS + List) :
```python
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        order = self.inOrder(root)
        for index in range(1, len(order)):
            if order[index] <= order[index-1]:
                return False
        return True

    def inOrder(self, node):
        if node is None:
            return

        result = []
        left = self.inOrder(node.left)
        if left:
            result += left

        result.append(node.val)

        right = self.inOrder(node.right)
        if right:
            result += right

        return result
```

Method 2 (Recursive In-Order DFS + List) :
```python
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        orders = []
        self.inOrder(root, orders)
        for index in range(1, len(orders)):
            if orders[index] <= orders[index-1]:
                return False

        return True

    def inOrder(self, node, orders):
        if node is None:
            return

        left = self.inOrder(node.left, orders)

        orders.append(node.val)

        right = self.inOrder(node.right, orders)
```

Method 3 (DFS + Interval By Values) :
```python
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        return self.dfs(root, float('-inf'), float('inf'))

    def dfs(self, node, minimum, maximum) -> bool:
        if node is None:
            return True

        current = node.val
        if current <= minimum or current >= maximum:
            return False

        return self.dfs(node.left, minimum, current) and self.dfs(node.right, current, maximum)
```

Method 4 (DFS + Interval By Nodes) :
```python
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        return self.dfs(root, None, None)

    def dfs(self, node, node_minimum, node_maximum) -> bool:
        if node is None:
            return True

        current = node.val
        # Option 1
        if (node_minimum and current <= node_minimum.val) or (node_maximum and current >= node_maximum.val):
            return False

        return self.dfs(node.left, node_minimum, node) and self.dfs(node.right, node, node_maximum)
        """
        # Option 2

        return (not node_minimum or current > node_minimum.val) and (not node_maximum or current < node_maximum.val) and self.dfs(node.left, node_minimum, node) and self.dfs(node.right, node, node_maximum)
        """
```

Method 5 (Iterative DFS, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        stack = [(root, float('-inf'), float('inf'))]
        while stack:
            node, minimum, maximum = stack.pop()

            if node.val <= minimum or node.val >= maximum:
                return False

            if node.left:
                stack.append((node.left, minimum, node.val))
            if node.right:
                stack.append((node.right, node.val, maximum))

        return True
```

Method 6 (Iterative In-Order DFS + Previous Node, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        node_previous = None
        stack = []

        node = root
        while True:
            while node:
                stack.append(node)
                node = node.left

            if len(stack) == 0:
                break

            node = stack.pop()
            # `previous node` is the node before ordered nodes' value by in-order traverse
            if node_previous and node.val <= node_previous.val:
                return False

            node_previous = node
            node = node.right

        return True
```

Method 7 (Morris Traversal, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def isValidBST(self, root: Optional[TreeNode]) -> bool:
        previous = -inf
        node = root
        while node:
            if node.left:
                node_friend = node.left
                while node_friend.right:
                    node_friend = node_friend.right

                node_friend.right = node

                node_temp = node.left
                node.left = None
                node = node_temp
                continue

            if node.val <= previous:
                return False

            previous = node.val
            node = node.right

        return True
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

Method 1 (In-Order + Record Values) :
```php
class Solution {

    /**
     * @param TreeNode $root
     * @return Boolean
     */
    function isValidBST($root) {
        $ordered = [];
        $this->inOrder($root, $ordered);
        for($index = 1; $index < count($ordered); $index++) {
            if ($ordered[$index] <= $ordered[$index-1]) {
                return false;
            }
        }

        return true;
    }

    function inOrder($node, &$ordered) {
        if (is_null($node)) {
            return;
        }

        $this->inOrder($node->left, $ordered);
        $ordered[] = $node->val;
        $this->inOrder($node->right, $ordered);
    }
}
```

Method 2 (DFS) :
```php
class Solution {

    /**
     * @param TreeNode $root
     * @return Boolean
     */
    function isValidBST($root) {
        return $this->dfs($root, PHP_INT_MIN, PHP_INT_MAX);
    }

    function dfs($node, $minimum, $maximum) {
        if (is_null($node)) {
            return true;
        }

        $current = $node->val;
        # Option 1
        if ($current <= $minimum || $current >= $maximum) {
            return false;
        }
        if ($this->dfs($node->left, $minimum, $current) == false) {
            return false;
        }
        if ($this->dfs($node->right, $current, $maximum) == false) {
            return false;
        }

        return true;
        /**
         * Option 2
         *
         * return $minimum < $current && $current < $maximum
         *   && $this->dfs($node->left, $minimum, $current)
         *   && $this->dfs($node->right, $current, $maximum);
         */
    }
}
```
