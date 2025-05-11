![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1550. [Three Consecutive Odds](https://leetcode.com/problems/three-consecutive-odds)

### Solution :

Method 1 (Greedy, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in `arr`)) :
```rust
impl Solution {
    pub fn three_consecutive_odds(arr: Vec<i32>) -> bool {
        let mut amount_cumulative: i32 = 0;
        for num in arr {
            if num % 2 == 0 {
                amount_cumulative = 0;
                continue;
            }

            amount_cumulative += 1;
            if amount_cumulative == 3 {
                return true
            }
        }

        return false
    }
}
```
