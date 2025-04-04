![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1123. [Lowest Common Ancestor Of Deepest Leaves](https://leetcode.com/problems/lowest-common-ancestor-of-deepest-leaves)

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

Method 1 (AI by Grok3, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of the elements in the tree)) :
```rust
use std::rc::Rc;
use std::cell::RefCell;

impl Solution {
    pub fn lca_deepest_leaves(root: Option<Rc<RefCell<TreeNode>>>) -> Option<Rc<RefCell<TreeNode>>> {
        fn dfs(node: &Option<Rc<RefCell<TreeNode>>>) -> (Option<Rc<RefCell<TreeNode>>>, i32) {
            match node {
                None => (None, 0), // Base case: null node, depth 0
                Some(node_ref) => {
                    let node = node_ref.borrow();
                    let (left_lca, left_depth) = dfs(&node.left);
                    let (right_lca, right_depth) = dfs(&node.right);

                    if left_depth == right_depth {
                        // If depths match, current node is LCA of deepest leaves
                        return (Some(Rc::clone(node_ref)), left_depth + 1)
                    } else if left_depth > right_depth {
                        // Left subtree has deeper leaves
                        return (left_lca, left_depth + 1)
                    } else {
                        // Right subtree has deeper leaves
                        return (right_lca, right_depth + 1)
                    }
                }
            }
        }

        let (lca, _) = dfs(&root);
        return lca
    }
}
```
