![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 897. [Increasing Order Search Tree](https://leetcode.com/problems/increasing-order-search-tree)

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

Method 1 (In-Order DFS + List, Time Complexity: $O(N)$ (N: amount of nodes), Space Complexity: $O(N)$) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
type Custom = Option<Rc<RefCell<TreeNode>>>;
impl Solution {
    pub fn increasing_bst(root: Custom) -> Custom {
        let mut nodes: Vec<i32> = vec![];
        Self::traverse(&mut nodes, root);
        if nodes.len() == 0 {
            return None
        }

        let mut result: Custom = Some(Rc::new(RefCell::new(TreeNode::new(nodes[0]))));
        let mut temp: Custom = result.clone();
        for val in nodes.into_iter().skip(1) {
            temp.as_ref().unwrap().borrow_mut().right = Some(Rc::new(RefCell::new(TreeNode::new(val))));
            temp = temp.unwrap().borrow().right.clone();
        }
        return result
    }

    fn traverse(nodes: &mut Vec<i32>, node: Custom) {
        /* Option 1 */
        return match node {
            None => (),
            Some(node) => {
                if node.borrow().left.is_none() && node.borrow().right.is_none() {
                    nodes.push(node.borrow().val);
                    return
                }

                if node.borrow().left.is_some() {
                    Self::traverse(nodes, node.borrow().left.clone());
                }
                nodes.push(node.borrow().val);
                if node.borrow().right.is_some() {
                    Self::traverse(nodes, node.borrow().right.clone());
                }
            },
        }
        /* Option 2

        return if let Some(node) = node {
            let node = node.borrow();
            if node.left.is_none() && node.right.is_none() {
                return nodes.push(node.val)
            }

            if node.left.is_some() {
                Self::traverse(nodes, node.left.clone());
            }
            nodes.push(node.val);
            if node.right.is_some() {
                Self::traverse(nodes, node.right.clone());
            }
        }
        */
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

Method 1 (In-Order DFS, Time Complexity: $O(N)$ (N: amount of nodes), Space Complexity: $O(D)$ (D: depth of binary search tree)) :
```python
class Solution:
    def increasingBST(self, root: TreeNode) -> TreeNode | None:
        result = None
        if root is None:
            return result

        if left := self.increasingBST(root.left):
            result = left

        current = TreeNode(root.val)
        if not result:
            pointer = result = current
        else:
            pointer = result
            while pointer.right:
                pointer = pointer.right
            pointer.right = current
            pointer = pointer.right

        if right := self.increasingBST(root.right):
            pointer.right = right

        return result
```
