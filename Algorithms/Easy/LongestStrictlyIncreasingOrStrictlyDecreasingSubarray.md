![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3105. [Longest Strictly Increasing Or Strictly Decreasing Subarray](https://leetcode.com/problems/longest-strictly-increasing-or-strictly-decreasing-subarray)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of elements in `nums`)) :
```rust
impl Solution {
    pub fn longest_monotonic_subarray(nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let mut result: i32 = 0;
        let mut left: usize = 0;
        let mut right: usize = 0;
        while right < n {
            result = i32::max(result, (right-left+1) as i32);
            right += 1;
            if right < n && nums[right-1] < nums[right] {
                continue;
            }

            left = right;
        }

        left = 0;
        right = 0;
        while left <= right && right < n {
            result = i32::max(result, (right-left+1) as i32);
            right += 1;
            if right < n && nums[right-1] > nums[right] {
                continue;
            }

            left = right;
        }

        return result
    }
}
```

Method 2 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of elements in `nums`)) :
```rust
impl Solution {
    pub fn longest_monotonic_subarray(nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let mut result: i32 = 0;
        let mut left_increasing: usize = 0;
        let mut left_decreasing: usize = 0;
        let mut right: usize = 0;
        while right < n {
            result = *[result, (right-left_increasing+1) as i32, (right-left_decreasing+1) as i32].iter().max().unwrap();
            right += 1;
            if right < n && nums[right-1] >= nums[right] {
                left_increasing = right;
            }
            if right < n && nums[right-1] <= nums[right] {
                left_decreasing = right;
            }
        }

        return result
    }
}
```
