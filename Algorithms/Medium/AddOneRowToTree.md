![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 623. [Add One Row To Tree](https://leetcode.com/problems/add-one-row-to-tree)

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

Method 1 (BFS, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
use std::collections::VecDeque;
type Custom = Option<Rc<RefCell<TreeNode>>>;
impl Solution {
    pub fn add_one_row(root: Custom, val: i32, depth: i32) -> Custom {
        if depth == 1 {
            let mut result: TreeNode = TreeNode::new(val);
            result.left = root;
            return Some(Rc::new(RefCell::new(result)))
        }

        let mut queue: VecDeque<(Custom, i32)> = VecDeque::from([(root.clone(), 1)]);
        while queue.len() > 0 {
            let (node, depth_current) = queue.pop_front().unwrap();
            if depth_current >= depth {
                break;
            }
            if node.is_none() {
                continue;
            }

            if depth_current == depth-1 {
                let mut node_left: TreeNode = TreeNode::new(val);
                let mut node_right: TreeNode = TreeNode::new(val);
                node_left.left = node.as_ref().unwrap().borrow().left.clone();
                node_right.right = node.as_ref().unwrap().borrow().right.clone();

                node.as_ref().unwrap().borrow_mut().left = Some(Rc::new(RefCell::new(node_left)));
                node.as_ref().unwrap().borrow_mut().right = Some(Rc::new(RefCell::new(node_right)));
            }

            queue.push_back((node.as_ref().unwrap().borrow().left.clone(), depth_current+1));
            queue.push_back((node.as_ref().unwrap().borrow().right.clone(), depth_current+1));
        }
        return root
    }
}
```

Method 2 (BFS + Readability Improvement, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
use std::collections::VecDeque;
type Custom = Option<Rc<RefCell<TreeNode>>>;
impl Solution {
    pub fn add_one_row(root: Custom, val: i32, depth: i32) -> Custom {
        if depth == 1 {
            let mut result: TreeNode = TreeNode::new(val);
            result.left = root;
            return Some(Rc::new(RefCell::new(result)))
        }

        let mut queue: VecDeque<(Custom, i32)> = VecDeque::from([(root.clone(), 1)]);
        while queue.len() > 0 {
            let (node, depth_current) = queue.pop_front().unwrap();
            if depth_current >= depth {
                break;
            }
            if node.is_none() {
                continue;
            }

            if depth_current == depth-1 {
                if let Some(&ref current) = node.as_ref() {
                    let mut node_left: TreeNode = TreeNode::new(val);
                    let mut node_right: TreeNode = TreeNode::new(val);

                    let mut current = current.borrow_mut();
                    node_left.left = current.left.take();
                    node_right.right = current.right.take();
                    current.left = Some(Rc::new(RefCell::new(node_left)));
                    current.right = Some(Rc::new(RefCell::new(node_right)));
                }
            }

            if let Some(&ref current) = node.as_ref() {
                let current = current.borrow();
                queue.push_back((current.left.clone(), depth_current+1));
                queue.push_back((current.right.clone(), depth_current+1));
            }
        }
        return root
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

Method 1 (BFS, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def addOneRow(self, root: Optional[TreeNode], val: int, depth: int) -> Optional[TreeNode]:
        if depth == 1:
            return TreeNode(val=val, left=root)

        queue = deque([(root, 1)])
        while queue:
            node, depth_current = queue.popleft()
            if node is None:
                continue
            if depth_current >= depth:
                break

            queue.append((node.left, depth_current+1))
            queue.append((node.right, depth_current+1))

            if depth_current == depth-1:
                node.left = TreeNode(val=val, left=node.left)
                node.right = TreeNode(val=val, right=node.right)

        return root
```
