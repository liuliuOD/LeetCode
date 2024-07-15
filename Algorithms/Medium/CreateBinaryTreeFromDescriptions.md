![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2196. [Create Binary Tree From Descriptions](https://leetcode.com/problems/pseudo-palindromic-paths-in-a-binary-tree)

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

Method 1 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: numbers of the elements in `descriptions`)) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
use std::collections::{HashMap, HashSet};
impl Solution {
    pub fn create_binary_tree(descriptions: Vec<Vec<i32>>) -> Option<Rc<RefCell<TreeNode>>> {
        let mut map: HashMap<i32, Rc<RefCell<TreeNode>>> = HashMap::new();
        let mut set: HashSet<i32> = HashSet::new();
        for description in descriptions {
            let parent = description[0];
            let value = description[1];
            let is_left = description[2];
            set.insert(value);
            if !map.contains_key(&parent) {
                map.insert(parent, Rc::new(RefCell::new(TreeNode::new(parent))));
            }
            if !map.contains_key(&value) {
                map.insert(value, Rc::new(RefCell::new(TreeNode::new(value))));
            }

            match is_left {
                0 => map.get_mut(&parent).unwrap().borrow_mut().right = Some(map.get(&value).unwrap().clone()),
                1 | _ => map.get_mut(&parent).unwrap().borrow_mut().left = Some(map.get(&value).unwrap().clone()),
            };
        }

        return Some(map.into_iter().filter(|item| !set.contains(&item.0)).last().unwrap().1)
    }
}
```

Method 2 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: numbers of the elements in `descriptions`)) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
use std::collections::{HashMap, HashSet};

type Custom = Rc<RefCell<TreeNode>>;
impl Solution {
    pub fn create_binary_tree(descriptions: Vec<Vec<i32>>) -> Option<Custom> {
        let mut map: HashMap<i32, Custom> = HashMap::new();
        let mut set: HashSet<i32> = HashSet::new();
        for description in descriptions {
            let parent = description[0];
            let value = description[1];
            let is_left = description[2];
            set.insert(value);

            let node_parent: Custom = map.entry(parent).or_insert(Rc::new(RefCell::new(TreeNode::new(parent)))).clone();
            let node_child: Custom = map.entry(value).or_insert(Rc::new(RefCell::new(TreeNode::new(value)))).clone();

            match is_left {
                0 => node_parent.borrow_mut().right = Some(node_child),
                1 | _ => node_parent.borrow_mut().left = Some(node_child),
            };
        }

        /* Option 1 */
        return Some(map.into_iter().filter(|item| !set.contains(&item.0)).last().unwrap().1)
        /* Option 2

        return Some(map.into_iter().find(|(key, _)| !set.contains(&key)).unwrap().1)
        */
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

Method 1 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: numbers of the elements in `descriptions`)) :
```python
class Solution:
    def createBinaryTree(self, descriptions: List[List[int]]) -> Optional[TreeNode]:
        candidates: dict[TreeNode] = dict()
        indegree: dict[int] = defaultdict(int)
        for parent, value, is_left in descriptions:
            indegree[value] += 1
            if parent not in candidates:
                candidates[parent] = TreeNode(val=parent)

            if value not in candidates:
                candidates[value] = TreeNode(val=value)

            if is_left:
                candidates[parent].left = candidates[value]
            else:
                candidates[parent].right = candidates[value]

        for node in candidates.keys():
            if node in indegree or indegree[node] > 0:
                continue

            return candidates[node]
        return None
```
