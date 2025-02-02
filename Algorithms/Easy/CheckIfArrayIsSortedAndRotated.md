![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1752. [Check If Array Is Sorted And Rotated](https://leetcode.com/problems/check-if-array-is-sorted-and-rotated)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of elements in `nums`)) :
```rust
impl Solution {
    pub fn check(nums: Vec<i32>) -> bool {
        let n: usize = nums.len();
        if n <= 1 {
            return true
        }

        let mut is_rotated: bool = false;
        for index in 1..n {
            if nums[index-1] <= nums[index] {
                continue;
            }

            if is_rotated {
                return false
            }
            is_rotated = true;
        }

        if is_rotated && *nums.last().unwrap() > nums[0] {
            return false
        }

        return true
    }
}
```
