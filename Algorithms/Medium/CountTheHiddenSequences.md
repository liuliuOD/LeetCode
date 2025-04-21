![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2145. [Count The Hidden Sequences](https://leetcode.com/problems/count-the-hidden-sequences)

### Solution :

Method 1 (AI by Grok3, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in `differences`)) :
```rust
impl Solution {
    pub fn number_of_arrays(differences: Vec<i32>, lower: i32, upper: i32) -> i32 {
        let mut min_val = 0;
        let mut max_val = 0;
        let mut curr = 0;

        // Calculate min and max values of the sequence
        for &diff in &differences {
            curr += diff as i64;
            min_val = min_val.min(curr);
            max_val = max_val.max(curr);
        }

        // Calculate the range of possible starting values
        let max_start = upper as i64 - max_val;
        let min_start = lower as i64 - min_val;

        // The number of valid arrays is the number of possible starting values
        let count = (max_start - min_start + 1).max(0);

        // Ensure the count fits within i32 and doesn't exceed the problem's constraints
        return count.min(1_000_000_007) as i32
    }
}
```
