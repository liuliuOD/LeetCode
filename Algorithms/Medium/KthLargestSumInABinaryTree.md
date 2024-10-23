![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2583. [Kth Largest Sum In A Binary Tree](https://leetcode.com/problems/kth-largest-sum-in-a-binary-tree)

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

Method 1 (DFS, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of the elements in the tree)) :
```rust
use std::rc::Rc;
use std::cell::RefCell;

type Custom = Rc<RefCell<TreeNode>>;

impl Solution {
    pub fn kth_largest_level_sum(root: Option<Custom>, k: i32) -> i64 {
        let mut counter: Vec<i64> = vec![0; 100_000+1];
        Self::traverse(root, 1, &mut counter);

        let mut indexes: Vec<usize> = Vec::from_iter((0..=100_000));
        indexes.sort_by_key(|index| -counter[*index]);

        return match counter[indexes[k as usize - 1]] {
            0 => -1,
            result => result,
        }
    }

    fn traverse(node: Option<Custom>, level: usize, counter: &mut Vec<i64>) {
        match node {
            None => {},
            Some(inner) => {
                counter[level] += inner.borrow().val as i64;

                Self::traverse(inner.borrow().left.clone(), level+1, counter);
                Self::traverse(inner.borrow().right.clone(), level+1, counter);
            },
        }
    }
}
```
