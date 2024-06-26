![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1382. [Balance A Binary Search Tree](https://leetcode.com/problems/balance-a-binary-search-tree)

### Solution :

```rust
// Definition for a binary tree node.
// #[derive(Debug, PartialEq, Eq)]
// pub struct TreeNode {
//   pub val: i32,
//   pub left: Option<Rc<RefCell<TreeNode>>>,
//   pub right: Option<Rc<RefCell<TreeNode>>>,
// }
//
// impl TreeNode {
//   #[inline]
//   pub fn new(val: i32) -> Self {
//     TreeNode {
//       val,
//       left: None,
//       right: None
//     }
//   }
// }
```

Method 1 (Iterative DFS + Array, Time Complexity: $O(N)$ (N: number of the nodes in the tree), Space Complexity: $O(N)$) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
type Custom = Option<Rc<RefCell<TreeNode>>>;
impl Solution {
    pub fn balance_bst(root: Custom) -> Custom {
        let ordered: Vec<i32> = Self::traverse(root.clone());

        return Self::build_tree(0, ordered.len()-1, &ordered)
    }

    fn traverse(node: Custom) -> Vec<i32> {
        let mut result: Vec<i32> = vec![];
        let mut stack: Vec<Custom> = vec![];
        let mut current: Custom = node.clone();
        while current.is_some() || stack.len() > 0 {
            let mut node_move = current.clone();
            while node_move.is_some() {
                stack.push(node_move.clone());
                node_move = node_move.unwrap().borrow().left.clone();
            }

            node_move = stack.pop().unwrap();
            if let Some(inner) = node_move {
                result.push(inner.borrow().val);
                current = inner.borrow().right.clone();
            }
        }

        return result
    }

    fn build_tree(index_left: usize, index_right: usize, ordered: &Vec<i32>) -> Custom {
        if index_left > index_right {
            return None
        }

        let index_middle: usize = index_left + (index_right - index_left)/2;
        let mut result = TreeNode::new(ordered[index_middle]);
        if index_middle < ordered.len()-1 {
            result.right = Self::build_tree(index_middle+1, index_right, ordered);
        }
        if index_middle > 0 {
            result.left = Self::build_tree(index_left, index_middle-1, ordered);
        }

        return Some(Rc::new(RefCell::new(result)))
    }
}
```

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (Recursive DFS + Array, Time Complexity: $O(N)$ (N: number of the nodes in the tree), Space Complexity: $O(N)$) :
```python
class Solution:
    def balanceBST(self, root: TreeNode) -> TreeNode:
        ordered = []
        self.traverse(root, ordered)

        return self.build_tree(ordered)

    def traverse(self, node: TreeNode, ordered: list[int]) -> None:
        if node.left is None and node.right is None:
            ordered.append(node.val)
            return

        if node.left:
            self.traverse(node.left, ordered)

        ordered.append(node.val)

        if node.right:
            self.traverse(node.right, ordered)

    def build_tree(self, ordered: list[int]) -> TreeNode | None:
        if not ordered:
            return None

        # Option 1
        if len(ordered) == 1:
            return TreeNode(val=ordered[0])
        """
        # Option 2
        """

        index_middle = len(ordered) // 2
        return TreeNode(val=ordered[index_middle], left=self.build_tree(ordered[:index_middle]), right=self.build_tree(ordered[index_middle+1:]))
```

Method 2 (Iterative DFS + Array, Time Complexity: $O(N)$ (N: number of the nodes in the tree), Space Complexity: $O(N)$) :
```python
class Solution:
    def balanceBST(self, root: TreeNode) -> TreeNode:
        ordered: list[int] = self.traverse(root)

        return self.build_tree(ordered)

    def traverse(self, node: TreeNode) -> list[int]:
        result = []
        stack = []
        current = node
        while stack or current:
            while current:
                stack.append(current)
                current = current.left

            current = stack.pop()
            result.append(current.val)
            current = current.right

        return result

    def build_tree(self, ordered: list[int]) -> TreeNode | None:
        if not ordered:
            return None

        index_middle = len(ordered) // 2
        return TreeNode(val=ordered[index_middle], left=self.build_tree(ordered[:index_middle]), right=self.build_tree(ordered[index_middle+1:]))
```
