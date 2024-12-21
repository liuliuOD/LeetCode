![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2415. [Reverse Odd Levels Of Binary Tree](https://leetcode.com/problems/reverse-odd-levels-of-binary-tree)

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

Method 1 (BFS, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of the elements in the tree)) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
use std::collections::VecDeque;
type Custom = Option<Rc<RefCell<TreeNode>>>;
impl Solution {
    pub fn reverse_odd_levels(root: Custom) -> Custom {
        let mut stack: Vec<i32> = Vec::new();
        let mut queue: VecDeque<(Custom, usize)> = VecDeque::from([(root.clone(), 0)]);
        while queue.len() > 0 {
            let item = queue.pop_front().unwrap();
            let mut node = item.0.as_ref().unwrap().borrow_mut();
            let level = item.1;
            if level % 2 == 1 {
                node.val = stack.pop().unwrap();
            }

            if node.left.is_none() || node.right.is_none() {
                continue;
            }

            if level % 2 == 0 {
                stack.push(node.left.as_ref().unwrap().borrow().val);
                stack.push(node.right.as_ref().unwrap().borrow().val);
            }

            queue.push_back((node.left.clone(), level+1));
            queue.push_back((node.right.clone(), level+1));
        }

        return root
    }
}
```

Method 2 (BFS, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of the elements in the tree)) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
use std::collections::VecDeque;
type Custom = Option<Rc<RefCell<TreeNode>>>;
impl Solution {
    pub fn reverse_odd_levels(root: Custom) -> Custom {
        let mut stack: Vec<i32> = Vec::new();
        let mut queue: VecDeque<Custom> = VecDeque::from([root.clone()]);
        let mut level: usize = 0;
        while queue.len() > 0 {
            for _ in 0..queue.len() {
                let item = queue.pop_front().unwrap();
                let mut node = item.as_ref().unwrap().borrow_mut();
                if level % 2 == 1 {
                    node.val = stack.pop().unwrap();
                }

                if node.left.is_none() || node.right.is_none() {
                    continue;
                }

                if level % 2 == 0 {
                    stack.push(node.left.as_ref().unwrap().borrow().val);
                    stack.push(node.right.as_ref().unwrap().borrow().val);
                }

                queue.push_back(node.left.clone());
                queue.push_back(node.right.clone());
            }

            level += 1;
        }

        return root
    }
}
```
