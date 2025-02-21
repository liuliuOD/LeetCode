![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1261. [Find Elements In A Contaminated Binary Tree](https://leetcode.com/problems/find-elements-in-a-contaminated-binary-tree)

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


/**
 * Your FindElements object will be instantiated and called as such:
 * let obj = FindElements::new(root);
 * let ret_1: bool = obj.find(target);
 */
```

Method 1 (Traverse, Time Complexity: $O(M*N)$, Space Complexity: $O(1)$ (M: the number of invocation times, N: the number of nodes in the tree)) :
```rust
use std::rc::Rc;
use std::cell::{RefCell, Ref, RefMut};

type Custom = Rc<RefCell<TreeNode>>;
struct FindElements {
    root: Option<Custom>,
}


/**
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
impl FindElements {

    fn new(root: Option<Custom>) -> Self {
        if root.is_some() {
            Self::traverse_build(root.clone(), 0);
        }

        return Self{
            root: root
        }
    }

    fn traverse_build(node: Option<Custom>, value: i32) {
        if node.is_none() {
            return
        }

        let mut inner: RefMut<'_, TreeNode> = node.as_ref().unwrap().borrow_mut();
        inner.val = value;
        if inner.left.is_some() {
            Self::traverse_build(inner.left.clone(), value*2 + 1);
        }
        if inner.right.is_some() {
            Self::traverse_build(inner.right.clone(), value*2 + 2);
        }
    }

    fn find(&self, target: i32) -> bool {
        return Self::traverse_find(self.root.clone(), target)
    }

    fn traverse_find(node: Option<Custom>, target: i32) -> bool {
        if node.is_none() {
            return false
        }

        let inner: Ref<'_, TreeNode> = node.as_ref().unwrap().borrow();
        if inner.val == target {
            return true
        }

        if inner.left.is_some() && Self::traverse_find(inner.left.clone(), target) {
            return true
        }
        if inner.right.is_some() && Self::traverse_find(inner.right.clone(), target) {
            return true
        }

        return false
    }
}
```

Method 2 (Traverse + Hash Set, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of nodes in the tree)) :
```rust

use std::rc::Rc;
use std::cell::{RefCell, Ref};
use std::collections::HashSet;

type Custom = Rc<RefCell<TreeNode>>;
struct FindElements {
    visited: HashSet<i32>,
}


/**
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
impl FindElements {

    fn new(root: Option<Custom>) -> Self {
        let mut visited: HashSet<i32> = HashSet::new();
        if root.is_some() {
            Self::traverse_build(&mut visited, root.clone(), 0);
        }

        return Self{
            visited: visited
        }
    }

    fn traverse_build(visited: &mut HashSet<i32>, node: Option<Custom>, value: i32) {
        if node.is_none() {
            return
        }

        let inner: Ref<'_, TreeNode> = node.as_ref().unwrap().borrow();
        visited.insert(value);
        if inner.left.is_some() {
            Self::traverse_build(visited, inner.left.clone(), value*2 + 1);
        }
        if inner.right.is_some() {
            Self::traverse_build(visited, inner.right.clone(), value*2 + 2);
        }
    }

    fn find(&self, target: i32) -> bool {
        return self.visited.contains(&target)
    }
}
```
