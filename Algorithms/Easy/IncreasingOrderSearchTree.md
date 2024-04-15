![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
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
    }
}
```
