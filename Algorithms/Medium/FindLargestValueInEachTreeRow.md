![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 515. [Find Largest Value In Each Tree Row](https://leetcode.com/problems/find-largest-value-in-each-tree-row)

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

Method 1 (BFS, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of nodes in the tree)) :
```rust

use std::rc::Rc;
use std::cell::RefCell;
use std::collections::VecDeque;

type Custom = Option<Rc<RefCell<TreeNode>>>;
impl Solution {
    pub fn largest_values(root: Custom) -> Vec<i32> {
        let mut result: Vec<i32> = Vec::new();
        if root.is_none() {
            return result
        }

        let mut queue: VecDeque<Custom> = VecDeque::from([root.clone()]);
        while queue.len() > 0 {
            let mut maximum: i32 = i32::MIN;
            for _ in 0..queue.len() {
                let node: Custom = queue.pop_front().unwrap();
                if node.is_none() {
                    continue;
                }

                let inner = node.as_ref().unwrap();
                maximum = i32::max(maximum, inner.borrow().val);
                if inner.borrow().left.is_some() {
                    queue.push_back(inner.borrow().left.clone());
                }
                if inner.borrow().right.is_some() {
                    queue.push_back(inner.borrow().right.clone());
                }
            }

            result.push(maximum);
        }

        return result
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

Method 1 (BFS) :
```python
class Solution:
    def largestValues(self, root: Optional[TreeNode]) -> List[int]:
        result = []
        # push `root` into queue when root exists
        queue = deque([root] if root else [])
        while queue:
            amount = len(queue)
            temp = -inf
            for _ in range(amount):
                node = queue.popleft()
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)

                temp = max(temp, node.val)

            result.append(temp)

        return result
```

Method 2 (BFS + Binary Heap) :
```python
class Solution:
    def largestValues(self, root: Optional[TreeNode]) -> List[int]:
        result = []
        queue = deque([root] if root else [])
        while queue:
            amount = len(queue)
            heap = []
            for _ in range(amount):
                node = queue.popleft()
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)

                heapq.heappush(heap, -node.val)

            result.append(-heapq.heappop(heap))

        return result
```

Method 3 (DFS) :
```python
class Solution:
    def largestValues(self, root: Optional[TreeNode]) -> List[int]:
        result = defaultdict(lambda: -inf)
        self.dfs(root, 0, result)
        return result.values()

    def dfs(self, node, depth, result):
        if node is None:
            return

        result[depth] = max(result[depth], node.val)
        self.dfs(node.left, depth+1, result)
        self.dfs(node.right, depth+1, result)
```
