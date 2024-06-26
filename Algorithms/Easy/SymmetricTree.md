![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 101. [Symmetric Tree](https://leetcode.com/problems/symmetric-tree)

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

Method 1 (DFS, Time Complexity: $O(N)$, Space Complexity: $O(H)$ (H: height of the tree)) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
type Custom = Option<Rc<RefCell<TreeNode>>>;
impl Solution {
    pub fn is_symmetric(root: Custom) -> bool {
        return match root {
            None => true,
            Some(node) => Self::traverse_and_compare(node.borrow().left.clone(), node.borrow().right.clone()),
        }
    }

    fn traverse_and_compare(node1: Custom, node2: Custom) -> bool {
        if node1.is_none() && node2.is_none() {
            return true
        }

        if (node1.is_none() && node2.is_some()) || (node1.is_some() && node2.is_none()) || node1.as_ref().unwrap().borrow().val != node2.as_ref().unwrap().borrow().val {
            return false
        }

        return Self::traverse_and_compare(node1.as_ref().unwrap().borrow().left.clone(), node2.as_ref().unwrap().borrow().right.clone()) && Self::traverse_and_compare(node1.as_ref().unwrap().borrow().right.clone(), node2.as_ref().unwrap().borrow().left.clone())
    }
}
```

Method 2 (DFS, Time Complexity: $O(N)$, Space Complexity: $O(H)$ (H: height of the tree)) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
type Custom = Option<Rc<RefCell<TreeNode>>>;
impl Solution {
    pub fn is_symmetric(root: Custom) -> bool {
        let left: Custom = root.as_ref().unwrap().borrow_mut().left.take();
        let right: Custom = root.as_ref().unwrap().borrow_mut().right.take();
        return Self::traverse_and_compare(left, right)
    }

    fn traverse_and_compare(node1: Custom, node2: Custom) -> bool {
        if node1.is_none() && node2.is_none() {
            return true
        }

        /* Option 1 */
        if (node1.is_none() && node2.is_some()) || (node1.is_some() && node2.is_none()) {
        /* Option 2

        if node1.is_none() || node2.is_none() {
        */
            return false
        }
        let mut inner1 = node1.as_ref().unwrap().borrow_mut();
        let mut inner2 = node2.as_ref().unwrap().borrow_mut();
        if inner1.val != inner2.val {
            return false
        }

        return Self::traverse_and_compare(inner1.left.take(), inner2.right.take()) && Self::traverse_and_compare(inner1.right.take(), inner2.left.take())
    }
}
```

Method 3 (BFS, Time Complexity: $O(N)$, Space Complexity: $O(H)$ (H: height of the tree)) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
use std::collections::VecDeque;
type Custom = Option<Rc<RefCell<TreeNode>>>;
impl Solution {
    pub fn is_symmetric(root: Custom) -> bool {
        let inner = root.as_ref().unwrap().borrow();
        let mut queue: VecDeque<(Custom, Custom)> = VecDeque::from([(inner.left.clone(), inner.right.clone())]);
        while queue.len() > 0 {
            let mut is_false: bool = false;
            match queue.pop_front().unwrap() {
                (None, None) => (),
                (Some(_), None) | (None, Some(_)) => is_false = true,
                (Some(inner1), Some(inner2)) => {
                    if inner1.borrow().val != inner2.borrow().val {
                        is_false = true;
                    }

                    queue.push_back((inner1.borrow().left.clone(), inner2.borrow().right.clone()));
                    queue.push_back((inner1.borrow().right.clone(), inner2.borrow().left.clone()));
                },
            }

            if is_false {
                return false
            }
        }

        return true
    }
}
```

### Solution :

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
```

Method 1 (DFS, Time Complexity: $O(N)$, Space Complexity: $O(H)$ (H: height of the tree)) :
```python
class Solution:
    def isSymmetric(self, root: Optional[TreeNode]) -> bool:
        self.result = True
        self.traverse(root.left, root.right)
        return self.result

    def traverse(self, node1, node2):
        if node1 is None and node2 is None:
            return
        if (node1 is None and node2 is not None) or (node1 is not None and node2 is None) or node1.val != node2.val:
            self.result = False
            return

        self.traverse(node1.left, node2.right)
        self.traverse(node1.right, node2.left)
```

Method 2 (BFS, Time Complexity: $O(N)$, Space Complexity: $O(H)$ (H: height of the tree)) :
```python
class Solution:
    def isSymmetric(self, root: Optional[TreeNode]) -> bool:
        queue = deque([(root.left, root.right)])
        while queue:
            node1, node2 = queue.popleft()
            if node1 is None and node2 is None:
                continue

            if node1 is None or node2 is None or node1.val != node2.val:
                return False

            queue.append((node1.left, node2.right))
            queue.append((node1.right, node2.left))

        return True
```
