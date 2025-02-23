![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1028. [Recover A Tree From Preorder Traversal](https://leetcode.com/problems/recover-a-tree-from-preorder-traversal)

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

Method 1 (DFS, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of elements in the tree)) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
type Custom = Rc<RefCell<TreeNode>>;
const BASE: u8 = b'0';

impl Solution {
    pub fn recover_from_preorder(traversal: String) -> Option<Custom> {
        let n: usize = traversal.len();
        let traversal_bytes: Vec<u8> = traversal.into_bytes();
        let mut val: i32 = 0;
        let mut index_current: usize = 0;
        while index_current < n && traversal_bytes[index_current] - BASE < 10 {
            val = val*10 + (traversal_bytes[index_current] - BASE) as i32;
            index_current += 1;
        }
        let mut root: Custom = Rc::new(RefCell::new(TreeNode::new(val)));
        if traversal_bytes.len() > 1 {
            Self::traverse(root.clone(), 0, &mut index_current, &traversal_bytes);
        }

        return Some(root)
    }

    fn traverse(node: Custom, depth: usize, index_traversal: &mut usize, traversal_bytes: &Vec<u8>) {
        let n: usize = traversal_bytes.len();

        if depth+1 > n-*index_traversal {
            return
        }
        if &traversal_bytes[*index_traversal..=*index_traversal+depth] == "-".repeat(depth+1).as_bytes() {
            let mut val: i32 = 0;
            let mut index_current: usize = *index_traversal + depth + 1;
            while index_current < n && traversal_bytes[index_current] - BASE < 10 {
                val = val*10 + (traversal_bytes[index_current] - BASE) as i32;
                index_current += 1;
            }

            node.borrow_mut().left = Some(Rc::new(RefCell::new(TreeNode::new(val))));
            *index_traversal = index_current;
            Self::traverse(node.borrow_mut().left.clone().unwrap(), depth+1, index_traversal, traversal_bytes);
        }

        if depth+1 > n-*index_traversal {
            return
        }
        if &traversal_bytes[*index_traversal..=*index_traversal+depth] == "-".repeat(depth+1).as_bytes() {
            let mut val: i32 = 0;
            let mut index_current: usize = *index_traversal + depth + 1;
            while index_current < n && traversal_bytes[index_current] - BASE < 10 {
                val = val*10 + (traversal_bytes[index_current] - BASE) as i32;
                index_current += 1;
            }

            node.borrow_mut().right = Some(Rc::new(RefCell::new(TreeNode::new(val))));
            *index_traversal = index_current;
            Self::traverse(node.borrow_mut().right.clone().unwrap(), depth+1, index_traversal, traversal_bytes);
        }
    }
}
```

Method 2 (DFS, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of elements in the tree)) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
type Custom = Rc<RefCell<TreeNode>>;
const BASE: u8 = b'0';

impl Solution {
    pub fn recover_from_preorder(traversal: String) -> Option<Custom> {
        let n: usize = traversal.len();
        let traversal_bytes: Vec<u8> = traversal.into_bytes();
        let index_and_value = Self::get_index_and_value(0, &traversal_bytes);
        let mut index_current: usize = index_and_value.0;
        let mut root: Custom = Rc::new(RefCell::new(TreeNode::new(index_and_value.1)));
        if traversal_bytes.len() > 1 {
            Self::traverse(root.clone(), 0, &mut index_current, &traversal_bytes);
        }

        return Some(root)
    }

    fn traverse(node: Custom, depth: usize, index_traversal: &mut usize, traversal_bytes: &Vec<u8>) {
        let n: usize = traversal_bytes.len();

        if depth+1 > n-*index_traversal {
            return
        }
        if &traversal_bytes[*index_traversal..=*index_traversal+depth] == "-".repeat(depth+1).as_bytes() {
            let index_and_value = Self::get_index_and_value(*index_traversal+depth+1, traversal_bytes);

            node.borrow_mut().left = Some(Rc::new(RefCell::new(TreeNode::new(index_and_value.1))));
            *index_traversal = index_and_value.0;
            Self::traverse(node.borrow_mut().left.clone().unwrap(), depth+1, index_traversal, traversal_bytes);
        }

        if depth+1 > n-*index_traversal {
            return
        }
        if &traversal_bytes[*index_traversal..=*index_traversal+depth] == "-".repeat(depth+1).as_bytes() {
            let index_and_value = Self::get_index_and_value(*index_traversal+depth+1, traversal_bytes);

            node.borrow_mut().right = Some(Rc::new(RefCell::new(TreeNode::new(index_and_value.1))));
            *index_traversal = index_and_value.0;
            Self::traverse(node.borrow_mut().right.clone().unwrap(), depth+1, index_traversal, traversal_bytes);
        }
    }

    fn get_index_and_value(mut index: usize, traversal_bytes: &Vec<u8>) -> (usize, i32) {
        let n: usize = traversal_bytes.len();
        let mut value: i32 = 0;
        while index < n && traversal_bytes[index] - BASE < 10 {
            value = value*10 + (traversal_bytes[index] - BASE) as i32;
            index += 1;
        }

        return (index, value)
    }
}
```

Method 3 (DFS, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of elements in the tree)) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
type Custom = Rc<RefCell<TreeNode>>;
const BASE: u8 = b'0';

impl Solution {
    pub fn recover_from_preorder(traversal: String) -> Option<Custom> {
        let n: usize = traversal.len();
        let traversal_bytes: &[u8] = traversal.as_bytes();
        let index_and_value = Self::get_index_and_value(0, traversal_bytes);
        let mut index_current: usize = index_and_value.0;
        let mut root: Custom = Rc::new(RefCell::new(TreeNode::new(index_and_value.1)));
        if traversal_bytes.len() > 1 {
            Self::traverse(root.clone(), 0, &mut index_current, traversal_bytes);
        }

        return Some(root)
    }

    fn traverse(node: Custom, depth: usize, index_traversal: &mut usize, traversal_bytes: &[u8]) {
        let n: usize = traversal_bytes.len();

        if depth+1 > n-*index_traversal {
            return
        }
        if &traversal_bytes[*index_traversal..=*index_traversal+depth] == "-".repeat(depth+1).as_bytes() {
            let index_and_value = Self::get_index_and_value(*index_traversal+depth+1, traversal_bytes);

            node.borrow_mut().left = Some(Rc::new(RefCell::new(TreeNode::new(index_and_value.1))));
            *index_traversal = index_and_value.0;
            Self::traverse(node.borrow_mut().left.clone().unwrap(), depth+1, index_traversal, traversal_bytes);
        }

        if depth+1 > n-*index_traversal {
            return
        }
        if &traversal_bytes[*index_traversal..=*index_traversal+depth] == "-".repeat(depth+1).as_bytes() {
            let index_and_value = Self::get_index_and_value(*index_traversal+depth+1, traversal_bytes);

            node.borrow_mut().right = Some(Rc::new(RefCell::new(TreeNode::new(index_and_value.1))));
            *index_traversal = index_and_value.0;
            Self::traverse(node.borrow_mut().right.clone().unwrap(), depth+1, index_traversal, traversal_bytes);
        }
    }

    fn get_index_and_value(mut index: usize, traversal_bytes: &[u8]) -> (usize, i32) {
        let n: usize = traversal_bytes.len();
        let mut value: i32 = 0;
        while index < n && traversal_bytes[index] - BASE < 10 {
            value = value*10 + (traversal_bytes[index] - BASE) as i32;
            index += 1;
        }

        return (index, value)
    }
}
```
