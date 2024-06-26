![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 94. [Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal)

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

Method 1 (two color marking method) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
impl Solution {
    pub fn inorder_traversal(root: Option<Rc<RefCell<TreeNode>>>) -> Vec<i32> {
        let mut result:Vec<i32> = vec![];

        let mut stack = vec![(root, false)];
        while stack.len() > 0 {
            if let Some((node, status)) = stack.pop() {
                if status {
                    result.push(node.unwrap().borrow().val);
                    continue;
                }

                if let Some(node) = node {
                    let ss = node.borrow();
                    stack.push((ss.right.clone(), false));
                    stack.push((Some(node.clone()), true));
                    stack.push((ss.left.clone(), false));
                }
            }
        }

        result
    }
}
```

Method 2 (two color marking method) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
impl Solution {
    pub fn inorder_traversal(root: Option<Rc<RefCell<TreeNode>>>) -> Vec<i32> {
        let mut result = vec![];
        let mut stack = vec![];
        stack.push((false, root));
        while !stack.is_empty() {
            let (visited, node) = stack.pop().unwrap();
            if visited {
                result.push(node.unwrap().borrow().val);
                continue;
            }
            match node {
                Some(ref_tree_node) => {
                    stack.push((false, ref_tree_node.borrow().right.clone()));
                    stack.push((true, Some(ref_tree_node.clone())));
                    stack.push((false, ref_tree_node.borrow().left.clone()));
                },
                None => (),
            }
        }

        result
    }
}
```

Method 3 (DFS) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
impl Solution {
    pub fn inorder_traversal(root: Option<Rc<RefCell<TreeNode>>>) -> Vec<i32> {
        let mut result = vec![];

        Self::inorder(&root, &mut result);

        result
    }

    fn inorder(node: &Option<Rc<RefCell<TreeNode>>>, result: &mut Vec<i32>) {
        match node {
            None => (),
            Some(rc_refcell_treenode) => {
                Self::inorder(&rc_refcell_treenode.borrow().left, result);
                result.push(rc_refcell_treenode.borrow().val);
                Self::inorder(&rc_refcell_treenode.borrow().right, result);
            },
        }
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

Method 1 (Recursive DFS, Time Complexity: $O(N)$ (N: number of the nodes in the tree), Space Complexity: $O(D)$ (D: depth of the tree)) :
```python
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        if root is None:
            return []
        if root.left is None and root.right is None:
            return [root.val]

        return self.inorderTraversal(root.left) + [root.val] + self.inorderTraversal(root.right)
```

Method 2 (Iterative DFS, Time Complexity: $O(N)$ (N: number of the nodes in the tree), Space Complexity: $O(D)$ (D: depth of the tree)) :
```python
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        result = []
        stack = []
        node = root
        while node or stack:
            while node:
                stack.append(node)
                node = node.left

            node = stack.pop()
            result.append(node.val)
            node = node.right

        return result
```

Method 3 (Morris Traversal, Time Complexity: $O(N)$ (N: number of the nodes in the tree), Space Complexity: $O(1)$) :
```python
class Solution:
    def inorderTraversal(self, root: Optional[TreeNode]) -> List[int]:
        result = []
        node = root
        while node:
            if node.left:
                node_current = node.left
                while node_current.right:
                    node_current = node_current.right

                node_current.right = node
                temp = node
                node = node.left
                temp.left = None
            else:
                result.append(node.val)
                node = node.right

        return result
```
