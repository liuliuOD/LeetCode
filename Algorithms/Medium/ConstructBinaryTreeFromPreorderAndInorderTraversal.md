![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 105. [Construct Binary Tree From Preorder And Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal)

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

### Solution :

Method 1 (Divide & Conquer + Hash Map, Time Complexity: $O(N)$) :
```python
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        mapping = {}
        for index, val in enumerate(inorder):
            mapping[val] = index

        n = len(preorder)
        return self.constructTree(0, n-1, 0, n-1, preorder, inorder, mapping)

    def constructTree(self, start_preorder, end_preorder, start_inorder, end_inorder, preorder, inorder, mapping) -> Optional[TreeNode]:
        if start_preorder > end_preorder or start_inorder > end_inorder:
            return None

        root_val = preorder[start_preorder]
        node = TreeNode(val=root_val)
        index_root_inorder = mapping[root_val]
        amount_left = index_root_inorder - start_inorder

        node.left = self.constructTree(start_preorder+1, start_preorder+amount_left, start_inorder, index_root_inorder-1, preorder, inorder, mapping)
        node.right = self.constructTree(start_preorder+amount_left+1, end_preorder, index_root_inorder+1, end_inorder, preorder, inorder, mapping)

        return node
```

Method 2 (Recursive, Time Complexity: $O(N^2)$) :
```python
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        if len(inorder) == 0:
            return None

        val_node = preorder.pop(0)
        index_node = inorder.index(val_node)

        return TreeNode(val_node, left=self.buildTree(preorder, inorder[:index_node]), right=self.buildTree(preorder, inorder[index_node+1:]))
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

Method 1 (Divide & Conquer + Hash Map) :
```php
class Solution {

    /**
     * @param Integer[] $preorder
     * @param Integer[] $inorder
     * @return TreeNode
     */
    function buildTree($preorder, $inorder) {
        $mapping = [];
        foreach($inorder as $index => $value) {
            $mapping[$value] = $index;
        }

        $n = count($preorder);
        return $this->divideAndConquer(0, $n-1, 0, $n-1, $preorder, $inorder, $mapping);
    }

    function divideAndConquer($indexPreorderStart, $indexPreorderEnd, $indexInorderStart, $indexInorderEnd, $preorder, $inorder, $mapping) {
        if ($indexPreorderStart > $indexPreorderEnd || $indexInorderStart > $indexInorderEnd) {
            return NULL;
        }

        $amountLeftSubtree = $mapping[$preorder[$indexPreorderStart]] - $indexInorderStart;
        $node = new TreeNode($preorder[$indexPreorderStart]);
        $node->left = $this->divideAndConquer($indexPreorderStart+1, $indexPreorderStart+$amountLeftSubtree, $indexInorderStart, $indexInorderStart+$amountLeftSubtree-1, $preorder, $inorder, $mapping);
        $node->right = $this->divideAndConquer($indexPreorderStart+$amountLeftSubtree+1, $indexPreorderEnd, $indexInorderStart+$amountLeftSubtree+1, $indexInorderEnd, $preorder, $inorder, $mapping);

        return $node;
    }
}
```
