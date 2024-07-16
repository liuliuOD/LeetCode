![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2096. [Step-By-Step Directions From A Binary Tree Node To Another](https://leetcode.com/problems/step-by-step-directions-from-a-binary-tree-node-to-another)

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

Method 1 (BFS, Time Complexity: $O(N)$, Space Complexity: $O(N^2)$ (N: number of the nodes in the tree)) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
use std::collections::VecDeque;
type Custom = Rc<RefCell<TreeNode>>;
impl Solution {
    pub fn get_directions(root: Option<Custom>, start_value: i32, dest_value: i32) -> String {
        let mut direction_start: String = Self::bfs(root.clone().unwrap(), start_value);
        let mut direction_dest: String = Self::bfs(root.clone().unwrap(), dest_value);

        let mut amount_the_same: usize = 0;
        for (char_1, char_2) in direction_start.chars().zip(direction_dest.chars()) {
            match char_1 == char_2 {
                true => amount_the_same += 1,
                false => break,
            };
        }

        return "U".repeat(direction_start.len()-amount_the_same) + &direction_dest[amount_the_same..]
    }

    fn bfs(node: Custom, value: i32) -> String {
        let mut queue: VecDeque<(Custom, String)> = VecDeque::from([(node, "".to_string())]);
        while queue.len() > 0 {
            let (current, direction) = queue.pop_front().unwrap();
            let inner = current.borrow();
            if inner.val == value {
                return direction
            }

            if inner.left.is_some() {
                queue.push_back((inner.left.clone().unwrap(), direction.clone()+"L"));
            }
            if inner.right.is_some() {
                queue.push_back((inner.right.clone().unwrap(), direction.clone()+"R"));
            }
        }

        return "".to_string()
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

Method 1 (BFS, Time Complexity: $O(N)$, Space Complexity: $O(N^2)$ (N: number of the nodes in the tree)) :
```python
class Solution:
    def getDirections(self, root: Optional[TreeNode], startValue: int, destValue: int) -> str:
        direction_start, direction_dest = "", ""
        direction_start = self.bfs(root, startValue)
        direction_dest = self.bfs(root, destValue)

        result = ""
        while direction_start and direction_dest:
            if direction_start[0] != direction_dest[0]:
                break

            direction_start = direction_start[1:]
            direction_dest = direction_dest[1:]

        return result + "U"*len(direction_start) + direction_dest

    def bfs(self, root: Optional[TreeNode], value: int) -> str:
        queue = deque([(root, "")])
        while queue:
            node, direction = queue.popleft()
            if node.val == value:
                return direction

            if node.left:
                queue.append((node.left, direction+"L"))
            if node.right:
                queue.append((node.right, direction+"R"))
```
