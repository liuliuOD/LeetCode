![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 962. [Maximum Width Ramp](https://leetcode.com/problems/maximum-width-ramp)

### Solution :

Method 1 (Sliding Window, ERROR: "Time Limit Exceeded", 98/101, Time Complexity: $O(N^2)$, Space Complexity: $O(1)$ (N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn max_width_ramp(nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        for window in (1..=n).rev() {
            for index_start in 0..=n-window {
                if nums[index_start] <= nums[index_start+window-1] {
                    return (window - 1) as i32
                }
            }
        }

        return 0
    }
}
```

Method 2 (Sorted, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn max_width_ramp(nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let mut sorted_index: Vec<i32> = Vec::from_iter(0..n as i32);
        sorted_index.sort_by_key(|index| (nums[*index as usize], *index));
        let mut result: i32 = 0;
        let mut index_minimum: i32 = n as i32;
        for index in sorted_index {
            result = i32::max(result, index - index_minimum);
            index_minimum = i32::min(index_minimum, index);
        }

        return result
    }
}
```
