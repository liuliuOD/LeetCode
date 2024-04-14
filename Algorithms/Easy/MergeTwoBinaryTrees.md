![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 617. [Merge Two Binary Trees](https://leetcode.com/problems/merge-two-binary-trees)

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

Method 1 (Time Complexity: $O(M+N)$ (M: amount of nodes in `root1`, N: amount of nodes in `root2`), Space Complexity: $O(M+N)$) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
impl Solution {
    pub fn merge_trees(root1: Option<Rc<RefCell<TreeNode>>>, root2: Option<Rc<RefCell<TreeNode>>>) -> Option<Rc<RefCell<TreeNode>>> {
        if root1.is_none() && root2.is_none() {
            return None
        }

        let mut result: Option<Rc<RefCell<TreeNode>>> = Some(Rc::new(RefCell::new(TreeNode::new(0))));
        Self::traverse(root1.clone(), &mut result);
        Self::traverse(root2.clone(), &mut result);
        return result
    }

    fn traverse(node: Option<Rc<RefCell<TreeNode>>>, result : &mut Option<Rc<RefCell<TreeNode>>>) {
        match node {
            None => (),
            Some(node) => {
                result.as_mut().unwrap().borrow_mut().val += node.borrow().val;
                if node.borrow().left.is_some() {
                    if result.as_ref().unwrap().borrow().left.is_none() {
                        result.as_mut().unwrap().borrow_mut().left = Some(Rc::new(RefCell::new(TreeNode::new(0))));
                    }
                        
                    Self::traverse(node.borrow().left.clone(), &mut result.as_mut().unwrap().borrow_mut().left);
                }
                if node.borrow().right.is_some() {
                    if result.as_ref().unwrap().borrow().right.is_none() {
                        result.as_mut().unwrap().borrow_mut().right = Some(Rc::new(RefCell::new(TreeNode::new(0))));
                    }

                    Self::traverse(node.borrow().right.clone(), &mut result.as_mut().unwrap().borrow_mut().right);
                }
            }
        }
    }
}
```
