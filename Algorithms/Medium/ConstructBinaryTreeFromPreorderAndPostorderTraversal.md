![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 889. [Construct Binary Tree From Preorder And Postorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-postorder-traversal)

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

Method 1 (Traverse, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of elements in `preorder`)) :
```rust
use std::rc::Rc;
use std::cell::{RefCell, RefMut};
type Custom = Rc<RefCell<TreeNode>>;

impl Solution {
    pub fn construct_from_pre_post(preorder: Vec<i32>, postorder: Vec<i32>) -> Option<Custom> {
        let mut index_preorder: usize = 0;
        let mut index_postorder: usize = 0;
        return Self::traverse(&mut index_preorder, &mut index_postorder, &preorder, &postorder)
    }

    fn traverse(index_preorder: &mut usize, index_postorder: &mut usize, preorder: &Vec<i32>, postorder: &Vec<i32>) -> Option<Custom> {
        let mut root: Option<Custom> = Some(Rc::new(RefCell::new(TreeNode::new(preorder[*index_preorder]))));
        *index_preorder += 1;

        let mut inner: RefMut<'_, TreeNode> = root.as_ref().unwrap().borrow_mut();
        if inner.val != postorder[*index_postorder] {
            inner.left = Self::traverse(index_preorder, index_postorder, preorder, postorder);
        }
        if inner.val != postorder[*index_postorder] {
            inner.right = Self::traverse(index_preorder, index_postorder, preorder, postorder);
        }

        *index_postorder += 1;

        return root.clone()
    }
}
```
