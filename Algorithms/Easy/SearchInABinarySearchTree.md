![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 700. [Search In A Binary Search Tree](https://leetcode.com/problems/search-in-a-binary-search-tree)

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

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(D)$ (D: depth of binary search tree)) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
impl Solution {
    pub fn search_bst(root: Option<Rc<RefCell<TreeNode>>>, val: i32) -> Option<Rc<RefCell<TreeNode>>> {
        return match root {
            None => None,
            Some(node) => {
                if node.borrow().val == val {
                    return Some(node.clone())
                } else if node.borrow().val < val {
                    return Self::search_bst(node.borrow().right.clone(), val)
                } else if val < node.borrow().val {
                    return Self::search_bst(node.borrow().left.clone(), val)
                }

                return None
            }
        }
    }
}
```

Method 2 (Time Complexity: $O(N)$, Space Complexity: $O(D)$ (D: depth of binary search tree)) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
impl Solution {
    pub fn search_bst(root: Option<Rc<RefCell<TreeNode>>>, val: i32) -> Option<Rc<RefCell<TreeNode>>> {
        return Self::traverse(root.clone(), val)
    }

    fn traverse(node: Option<Rc<RefCell<TreeNode>>>, val: i32) -> Option<Rc<RefCell<TreeNode>>> {
        return match node {
            None => None,
            Some(node) => {
                if node.borrow().val == val {
                    return Some(node.clone())
                } else if node.borrow().val < val {
                    return Self::traverse(node.borrow().right.clone(), val)
                } else if val < node.borrow().val {
                    return Self::traverse(node.borrow().left.clone(), val)
                }

                return None
            }
        }
    }
}
```
