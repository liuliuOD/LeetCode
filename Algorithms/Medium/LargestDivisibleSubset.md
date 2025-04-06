![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 368. [Largest Divisible Subset](https://leetcode.com/problems/largest-divisible-subset)

### Solution :

Method 1 (AI by Grok3, Dynamic Programming, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn largest_divisible_subset(mut nums: Vec<i32>) -> Vec<i32> {
        let n = nums.len();
        if n == 0 {
            return vec![];
        }

        // Sort the array
        nums.sort_unstable();

        // dp[i]: size of largest subset ending at i
        // prev[i]: previous index in the subset
        let mut dp = vec![1; n];
        let mut prev = vec![-1; n];
        let mut max_size = 1;
        let mut max_index = 0;

        // Fill DP table
        for i in 1..n {
            for j in 0..i {
                if nums[i] % nums[j] == 0 && dp[j] + 1 > dp[i] {
                    dp[i] = dp[j] + 1;
                    prev[i] = j as i32;
                    if dp[i] > max_size {
                        max_size = dp[i];
                        max_index = i;
                    }
                }
            }
        }

        // Reconstruct the subset
        let mut result = Vec::new();
        let mut curr = max_index as i32;
        while curr != -1 {
            result.push(nums[curr as usize]);
            curr = prev[curr as usize];
        }

        return result
    }
}
```
