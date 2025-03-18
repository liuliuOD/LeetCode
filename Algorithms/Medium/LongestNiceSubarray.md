![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2401. [Longest Nice Subarray](https://leetcode.com/problems/longest-nice-subarray)

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of elements in `nums`)) :
```rust
impl Solution {
    pub fn longest_nice_subarray(nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let mut bit_xor: i32 = 0;
        let mut start: usize = 0;
        let mut result: i32 = 0;
        for end in 0..n {
            while (bit_xor & nums[end]) != 0 {
                bit_xor ^= nums[start];
                start += 1;
            }

            bit_xor |= nums[end];
            result = i32::max(result, (end - start + 1) as i32);
        }

        return result
    }
}
```
