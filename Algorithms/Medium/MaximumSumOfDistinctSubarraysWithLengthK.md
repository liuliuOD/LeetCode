![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2461. [Maximum Sum Of Distinct Subarrays With Length K](https://leetcode.com/problems/maximum-sum-of-distinct-subarrays-with-length-k)

### Solution :

Method 1 (Two Pointer + Hash Set, Time Complexity: $O(N)$, Space Complexity: $O(K)$ (N: the number of the elements in `nums`, K: the value of `k`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn maximum_subarray_sum(nums: Vec<i32>, k: i32) -> i64 {
        let mut set: HashSet<i32> = HashSet::new();
        let mut result: i64 = 0;
        let mut sum: i64 = 0;
        let mut left: usize = 0;
        for right in 0..nums.len() {
            while set.contains(&nums[right]) || (right-left) as i32 >= k {
                set.remove(&nums[left]);
                sum -= nums[left] as i64;
                left += 1;
            }
            set.insert(nums[right]);
            sum += nums[right] as i64;

            if (right-left+1) as i32 == k {
                result = i64::max(result, sum);
            }
        }

        return result
    }
}
```
