![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2537. [Count The Number Of Good Subarrays](https://leetcode.com/problems/count-the-number-of-good-subarrays)

### Solution :

Method 1 (AI by Grok3, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of elements in `nums`)) :
```rust
impl Solution {
    pub fn count_good(nums: Vec<i32>, k: i32) -> i64 {
        let k = k as i64;
        let mut count = 0;
        let mut freq = std::collections::HashMap::new();
        let mut pairs: i64 = 0;
        let mut left = 0;

        for right in 0..nums.len() {
            // Update frequency and pairs for current number
            let num = nums[right];
            let prev_freq = *freq.get(&num).unwrap_or(&0);
            pairs += prev_freq as i64;
            freq.insert(num, prev_freq + 1);

            // Shrink window while pairs >= k
            while pairs >= k && left <= right {
                count += (nums.len() - right) as i64;

                // Remove leftmost element
                let left_num = nums[left];
                let left_freq = freq.get(&left_num).unwrap() - 1;
                pairs -= left_freq as i64;
                if left_freq == 0 {
                    freq.remove(&left_num);
                } else {
                    freq.insert(left_num, left_freq);
                }
                left += 1;
            }
        }

        return count
    }
}
```
