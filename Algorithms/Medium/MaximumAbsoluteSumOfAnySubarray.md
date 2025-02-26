![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1749. [Maximum Absolute Sum Of Any Subarray](https://leetcode.com/problems/maximum-absolute-sum-of-any-subarray)

### Solution :

Method 1 (Prefix Sum, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of elements in `nums`)) :
```rust
impl Solution {
    pub fn max_absolute_sum(nums: Vec<i32>) -> i32 {
        let mut result: i32 = 0;
        let mut prefix_sum: i32 = 0;
        let mut minimum: i32 = 0;
        let mut maximum: i32 = 0;
        for num in nums {
            prefix_sum += num;
            minimum = i32::min(minimum, prefix_sum);
            maximum = i32::max(maximum, prefix_sum);

            if prefix_sum < 0 {
                result = i32::max(result, i32::max(prefix_sum.abs(), (prefix_sum-maximum).abs()));
            } else {
                result = i32::max(result, i32::max(prefix_sum, prefix_sum-minimum));
            }
        }

        return result
    }
}
```
