![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2471. [Minimum Number Of Operations To Sort A Binary Tree By Level](https://leetcode.com/problems/minimum-number-of-operations-to-sort-a-binary-tree-by-level)

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

Method 1 (BFS + Hash Map, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of the elements in the tree)) :
```rust
use std::rc::Rc;
use std::cell::RefCell;
use std::collections::{HashMap, VecDeque};

type Custom = Option<Rc<RefCell<TreeNode>>>;
impl Solution {
    pub fn minimum_operations(root: Custom) -> i32 {
        let mut queue: VecDeque<Custom> = VecDeque::from([root.clone()]);
        let mut result: i32 = 0;
        while queue.len() > 0 {
            let mut nums: Vec<i32> = Vec::new();
            for _ in 0..queue.len() {
                let element: Custom = queue.pop_front().unwrap();
                if element.is_none() {
                    continue;
                }

                let node = element.as_ref().unwrap();
                let inner = node.borrow();
                if inner.left.is_some() {
                    queue.push_back(inner.left.clone());
                    nums.push(inner.left.as_ref().unwrap().borrow().val);
                }
                if inner.right.is_some() {
                    queue.push_back(inner.right.clone());
                    nums.push(inner.right.as_ref().unwrap().borrow().val);
                }
            }

            let mut mapping: HashMap<i32, usize> = HashMap::new();
            for (index, &value) in nums.iter().enumerate() {
                mapping.entry(value).or_insert(index);
            }

            let mut nums_sorted = nums.clone();
            nums_sorted.sort();
            for index in 0..nums.len() {
                if nums[index] == nums_sorted[index] {
                    continue;
                }

                result += 1;
                let index_mapping: usize = *mapping.get(&nums_sorted[index]).unwrap();
                nums[index_mapping] = nums[index];
                mapping.entry(nums[index]).and_modify(|item| *item = index_mapping);
            }
        }

        return result
    }
}
```
