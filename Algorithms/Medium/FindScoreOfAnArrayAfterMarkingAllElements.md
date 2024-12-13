![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2593. [Find Score Of An Array After Marking All Elements](https://leetcode.com/problems/find-score-of-an-array-after-marking-all-elements)

### Solution :

Method 1 (Minimum Binary Heap, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of the elements in `nums`)) :
```rust
use std::collections::{BinaryHeap, HashSet};
use std::cmp::Reverse;

impl Solution {
    pub fn find_score(nums: Vec<i32>) -> i64 {
        let n: usize = nums.len();
        let mut heap: BinaryHeap<(Reverse<i32>, Reverse<usize>)> = BinaryHeap::from_iter(nums.into_iter().enumerate().map(|(index, num)| (Reverse(num), Reverse(index))));
        let mut visited: HashSet<usize> = HashSet::new();
        let mut result: i64 = 0;
        while heap.len() > 0 {
            let (Reverse(num), Reverse(index)) = heap.pop().unwrap();
            if visited.contains(&index) {
                continue;
            }

            if index > 0 {
                visited.insert(index-1);
            }
            if index < n-1 {
                visited.insert(index+1);
            }
            result += num as i64;
        }

        return result
    }
}
```
