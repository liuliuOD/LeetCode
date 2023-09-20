![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 102. [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal)

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (BFS) :
```python
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        result = defaultdict(list)
        queue = deque([(root, 0)])
        while queue:
            node, level = queue.popleft()
            if node is None:
                continue

            result[level].append(node.val)

            queue.append((node.left, level+1))
            queue.append((node.right, level+1))

        return result.values()
```

Method 2 (BFS) :
```python
class Solution:
    def levelOrder(self, root: Optional[TreeNode]) -> List[List[int]]:
        result = []
        queue = deque([root])
        while queue:
            amount = len(queue)
            group = []
            while amount:
                amount -= 1
                node = queue.popleft()
                if node is None:
                    continue

                group.append(node.val)

                queue.append(node.left)
                queue.append(node.right)

            if len(group):
                result.append(group)

        return result
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

Method 1 (BFS) :
```php
class Solution {

    /**
     * @param TreeNode $root
     * @return Integer[][]
     */
    function levelOrder($root) {
        $result = [];
        $queue = new SplQueue();
        $queue->enqueue([$root, 0]);
        while($queue->count()) {
            list($node, $level) = $queue->dequeue();
            if (is_null($node)) {
                continue;
            }

            isset($result[$level])
                ? $result[$level][] = $node->val
                : $result[$level] = [$node->val];
            
            $queue->enqueue([$node->left, $level+1]);
            $queue->enqueue([$node->right, $level+1]);
        }

        return $result;
    }
}
```

Method 2 (BFS) :
```php
class Solution {

    /**
     * @param TreeNode $root
     * @return Integer[][]
     */
    function levelOrder($root) {
        $result = [];
        $queue = new SplQueue();
        $queue->enqueue($root);
        while ($queue->count()) {
            $amount = $queue->count();
            $group = [];
            while ($amount--) {
                $node = $queue->dequeue();
                if (is_null($node)) {
                    continue;
                }

                $group[] = $node->val;
                $queue->enqueue($node->left);
                $queue->enqueue($node->right);
            }

            if (count($group)) {
                $result[] = $group;
            }
        }

        return $result;
    }
}
```
