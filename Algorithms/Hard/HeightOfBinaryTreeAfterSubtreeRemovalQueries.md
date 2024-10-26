![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2458. [Height Of Binary Tree After Subtree Removal Queries](https://leetcode.com/problems/height-of-binary-tree-after-subtree-removal-queries)

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

Method 1 (DFS, Time Complexity: $O(N+Q)$, Space Complexity: $O(N)$ (N: the number of the elements in the tree, Q: the value of `queries`)) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
use std::collections::VecDeque;

type Custom = Rc<RefCell<TreeNode>>;
impl Solution {
    pub fn tree_queries(root: Option<Custom>, queries: Vec<i32>) -> Vec<i32> {
        let mut depth_maximum_without_current: [i32; 100_001] = [0; 100_001];
        Self::traverse(root.clone(), 0, &mut 0, &mut depth_maximum_without_current, true);
        Self::traverse(root.clone(), 0, &mut 0, &mut depth_maximum_without_current, false);

        return queries.iter().map(|query| depth_maximum_without_current[*query as usize]).collect()
    }

    fn traverse(node: Option<Custom>, depth: i32, depth_maximum: &mut i32, depth_maximum_without_current: &mut [i32; 100_001], from_left: bool) {
        match node {
            None => {},
            Some(inner) => {
                let val_current: usize = inner.borrow().val as usize;
                depth_maximum_without_current[val_current] = i32::max(depth_maximum_without_current[val_current], *depth_maximum);

                *depth_maximum = i32::max(*depth_maximum, depth);

                if from_left {
                    Self::traverse(inner.borrow().left.clone(), depth+1, depth_maximum, depth_maximum_without_current, from_left);
                    Self::traverse(inner.borrow().right.clone(), depth+1, depth_maximum, depth_maximum_without_current, from_left);
                } else {
                    Self::traverse(inner.borrow().right.clone(), depth+1, depth_maximum, depth_maximum_without_current, from_left);
                    Self::traverse(inner.borrow().left.clone(), depth+1, depth_maximum, depth_maximum_without_current, from_left);
                }
            }
        }
    }
}
```
