![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2529. [Maximum Count Of Positive Integer And Negative Integer](https://leetcode.com/problems/maximum-count-of-positive-integer-and-negative-integer)

### Solution :

Method 1 (Brute Force + Optimization, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of elements in `nums`)) :
```rust
impl Solution {
    pub fn maximum_count(nums: Vec<i32>) -> i32 {
        let n: i32 = nums.len() as i32;
        let mut amount_negative: i32 = 0;
        let mut amount_positive: i32 = 0;
        for (index, num) in nums.into_iter().enumerate() {
            if num < 0 {
                amount_negative += 1;
            } else if num > 0 {
                amount_positive = n - index as i32;
                break;
            }
        }

        return i32::max(amount_negative, amount_positive)
    }
}
```

Method 2 (Binary Search, Time Complexity: $O(Log(N))$, Space Complexity: $O(1)$ (N: the number of elements in `nums`)) :
```rust
impl Solution {
    pub fn maximum_count(nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let mut left: usize = 0;
        let mut right: usize = n;
        while left < right {
            let middle: usize = left + (right-left)/2;
            if nums[middle] < 0 {
                left = middle + 1;
            } else {
                right = middle;
            }
        }
        let amount_negative: i32 = right as i32;

        left = 0;
        right = n;
        while left < right {
            let middle: usize = left + (right-left)/2;
            if nums[middle] <= 0 {
                left = middle + 1;
            } else {
                right = middle;
            }
        }
        let amount_positive: i32 = (n - right) as i32;

        return i32::max(amount_negative, amount_positive)
    }
}
```

Method 3 (AI by Grok3, Binary Search, Time Complexity: $O(Log(N))$, Space Complexity: $O(1)$ (N: the number of elements in `nums`)) :
```rust
impl Solution {
    pub fn maximum_count(nums: Vec<i32>) -> i32 {
        // Use binary search to find first non-negative number (count of negatives)
        let neg_count = nums.partition_point(|&x| x < 0) as i32;

        // Use binary search to find first positive number, subtract negatives and zeros
        let pos_count = nums.len() as i32 - nums.partition_point(|&x| x <= 0) as i32;

        neg_count.max(pos_count)
    }
}
```
