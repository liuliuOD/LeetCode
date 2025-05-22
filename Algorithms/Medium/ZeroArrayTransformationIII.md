![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3362. [Zero Array Transformation III](https://leetcode.com/problems/zero-array-transformation-iii)

### Solution :

Method 1 (Prefix Sum, Time Complexity: $O(M*Log(M)+N)$, Space Complexity: $O(M+N)$ (M: the number of the elements in `queries`, N: the number of the elements in `nums`)) :
```rust
use std::collections::BinaryHeap;

impl Solution {
    pub fn max_removal(nums: Vec<i32>, mut queries: Vec<Vec<i32>>) -> i32 {
        queries.sort();
        let n: usize = nums.len();
        let m: usize = queries.len();
        let mut heap: BinaryHeap<usize> = BinaryHeap::new();
        let mut cumulative: i32 = 0;
        let mut cumulative_sum: Vec<i32> = vec![0; n+1];
        let mut index_query: usize = 0;
        for index_num in 0..n {
            cumulative += cumulative_sum[index_num];
            while index_query < m && queries[index_query][0] as usize == index_num {
                heap.push(queries[index_query][1] as usize);
                index_query += 1;
            }

            let num: i32 = nums[index_num];
            while cumulative < num && heap.len() > 0 && *heap.peek().unwrap() >= index_num {
                cumulative += 1;
                cumulative_sum[heap.pop().unwrap() + 1] -= 1;
            }

            if cumulative < num {
                return -1
            }
        }

        return heap.len() as i32
    }
}
```
