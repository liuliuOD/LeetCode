![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 104. [Maximum Depth Of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree)

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
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        self.result = 0
        self.dfs(root, 1)
        return self.result

    def dfs(self, node, level):
        if node is None:
            self.result = max(self.result, level-1)
            return None

        self.dfs(node.left, level+1)
        self.dfs(node.right, level+1)
```

Method 2 (BFS) :
```python
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if root is None:
            return 0

        result = 0
        queue = deque([root])
        while queue:
            result += 1
            amount = len(queue)
            for _ in range(amount):
                node = queue.popleft()
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)

        return result
```

Method 3 (Recursive) :
```python
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if root is None:
            return 0

        return 1 + max(self.maxDepth(root.left), self.maxDepth(root.right))
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
     * @param TreeNode $root
     * @return Integer
     */
    function maxDepth($root) {
        if (is_null($root)) {
            return 0;
        }

        return 1 + max($this->maxDepth($root->left), $this->maxDepth($root->right));
    }
}
```

Method 2 (BFS) :
```php
class Solution {

    /**
     * @param TreeNode $root
     * @return Integer
     */
    function maxDepth($root) {
        if (is_null($root)) {
            return 0;
        }

        $result = 0;
        $queue = new SplQueue();
        $queue->enqueue($root);
        while ($queue->count()) {
            $result++;
            $amount = $queue->count();
            for ($_ = 0; $_ < $amount; $_++) {
                $node = $queue->dequeue();

                if ($node->left) {
                    $queue->enqueue($node->left);
                }
                if ($node->right) {
                    $queue->enqueue($node->right);
                }
            }
        }

        return $result;
    }
}
```
