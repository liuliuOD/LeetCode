![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1110. [Delete Nodes And Return Forest](https://leetcode.com/problems/delete-nodes-and-return-forest)

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

Method 1 (BFS + Hash Set) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
use std::collections::{VecDeque, HashSet};
type Custom = Rc<RefCell<TreeNode>>;
impl Solution {
    pub fn del_nodes(root: Option<Custom>, to_delete: Vec<i32>) -> Vec<Option<Custom>> {
        let mut result: Vec<Option<Custom>> = Vec::new();
        if root.is_none() {
            return result
        }

        let set: HashSet<i32> = HashSet::from_iter(to_delete);
        let mut dummy_node: TreeNode = TreeNode::new(0);
        dummy_node.left = root.clone();
        let mut queue: VecDeque<(Custom, bool)> = VecDeque::from([(Rc::new(RefCell::new(dummy_node)), true)]);
        while queue.len() > 0 {
            let (node, is_parent_deleted) = queue.pop_front().unwrap();
            let mut inner = node.borrow_mut();
            if inner.left.is_some() {
                if set.contains(&inner.left.clone().unwrap().borrow().val) {
                    queue.push_back((inner.left.clone().unwrap(), true));
                    inner.left = None;
                } else {
                    queue.push_back((inner.left.clone().unwrap(), false));
                    if is_parent_deleted {
                        result.push(inner.left.clone());
                    }
                }
            }

            if inner.right.is_some() {
                if set.contains(&inner.right.clone().unwrap().borrow().val) {
                    queue.push_back((inner.right.clone().unwrap(), true));
                    inner.right = None;
                } else {
                    queue.push_back((inner.right.clone().unwrap(), false));
                    if is_parent_deleted {
                        result.push(inner.right.clone());
                    }
                }
            }
        }

        return result
    }
}
```
