![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 632. [Smallest Range Covering Elements From K Lists](https://leetcode.com/problems/smallest-range-covering-elements-from-k-lists)

### Solution :

Method 1 (Multi Pointer, Time Complexity: $O(M*N)$, Space Complexity: $O(N)$ (M: the average number of each element in `nums`, N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn smallest_range(nums: Vec<Vec<i32>>) -> Vec<i32> {
        let n: usize = nums.len();
        let mut pointers: Vec<usize> = vec![0; n];
        let mut result: Vec<i32> = Vec::from([i32::MAX, i32::MIN]);
        loop {
            let mut index_minimum: usize = 0;
            let mut current: Vec<i32> = Vec::from([i32::MAX, i32::MIN]);
            for index in 0..n {
                let index_current: usize = pointers[index];
                if index_current >= nums[index].len() {
                    return result
                }

                let current_num: i32 = nums[index][index_current];
                current[0] = i32::min(current[0], current_num);
                current[1] = i32::max(current[1], current_num);

                if current_num < nums[index_minimum][pointers[index_minimum]] {
                    index_minimum = index;
                }
            }
            pointers[index_minimum] += 1;

            let range_current: i32 = current[1] - current[0];
            let range_result: i32 = result[1] - result[0];
            if result[0] == i32::MAX || (range_current < range_result) || (range_current == range_result && current[0] < result[0]) {
                result = current;
            }
        }

        unreachable!();
    }
}
```
