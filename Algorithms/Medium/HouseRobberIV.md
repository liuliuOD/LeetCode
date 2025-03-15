![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2560. [House Robber IV](https://leetcode.com/problems/house-robber-iv)

### Solution :

Method 1 (AI by Grok3, Binary Search, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(1)$ (K: the value of `k`, N: the number of elements in `nums`)) :
```rust
impl Solution {
    pub fn min_capability(nums: Vec<i32>, k: i32) -> i32 {
        let mut left = *nums.iter().min().unwrap();
        let mut right = *nums.iter().max().unwrap();

        // Binary search on capability
        while left < right {
            let mid = left + (right - left) / 2;

            // Count how many houses can be robbed with capability 'mid'
            let mut count = 0;
            let mut i = 0;
            while i < nums.len() {
                if nums[i] <= mid {
                    count += 1;
                    i += 2; // Skip the next house
                } else {
                    i += 1; // Move to next house
                }
            }

            // If we can rob k or more houses, try a lower capability
            if count >= k {
                right = mid;
            } else {
                left = mid + 1;
            }
        }

        return left // Final answer
    }
}
```

Method 2 (AI by Grok3, Binary Search, Time Complexity: $O(K*Log(N))$, Space Complexity: $O(1)$ (K: the value of `k`, N: the number of elements in `nums`)) :
```rust
impl Solution {
    pub fn min_capability(nums: Vec<i32>, k: i32) -> i32 {
        let mut left = *nums.iter().min().unwrap();
        let mut right = *nums.iter().max().unwrap();

        // Binary search on capability
        while left < right {
            let mid = left + (right - left) / 2;

            // Count how many houses can be robbed with capability 'mid'
            let mut count = 0;
            let mut i = 0;
            while i < nums.len() {
                if nums[i] <= mid {
                    count += 1;
                    if count >= k {
                        break
                    }

                    i += 2; // Skip the next house
                } else {
                    i += 1; // Move to next house
                }
            }

            // If we can rob k or more houses, try a lower capability
            if count >= k {
                right = mid;
            } else {
                left = mid + 1;
            }
        }

        return left // Final answer
    }
}
```
