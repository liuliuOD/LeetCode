![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2641. [Cousins In Binary Tree II](https://leetcode.com/problems/cousins-in-binary-tree-ii)

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
    pub fn replace_value_in_tree(root: Option<Custom>) -> Option<Custom> {
        let mut counter: Vec<i32> = vec![0; 100_000+1];
        Self::traverse(root.clone(), 0, &mut counter);
        
        let mut node: TreeNode = TreeNode::new(0);
        node.left = root.clone();
        let node_dummy: Option<Custom> = Some(Rc::new(RefCell::new(node)));
        Self::replace(node_dummy, 0, &counter);

        return root
    }

    fn traverse(node: Option<Custom>, level: usize, counter: &mut Vec<i32>) {
        match node {
            None => {},
            Some(inner) => {
                counter[level] += inner.borrow().val;

                Self::traverse(inner.borrow().left.clone(), level+1, counter);
                Self::traverse(inner.borrow().right.clone(), level+1, counter);
            },
        }
    }

    fn replace(node: Option<Custom>, level: usize, counter: &Vec<i32>) {
        match node {
            None => {},
            Some(inner) => {
                let node_left = inner.borrow().left.clone();
                let node_right = inner.borrow().right.clone();

                let mut sum_level: i32 = counter[level];
                if let Some(ref inner) = node_left {
                    sum_level -= inner.borrow().val;
                }
                if let Some(ref inner) = node_right {
                    sum_level -= inner.borrow().val;
                }

                if let Some(ref inner) = node_left {
                    inner.borrow_mut().val = sum_level;
                }
                if let Some(ref inner) = node_right {
                    inner.borrow_mut().val = sum_level;
                }

                Self::replace(node_left, level+1, counter);
                Self::replace(node_right, level+1, counter);
            },
        }
    }
}
```
