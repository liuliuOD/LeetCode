![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1550. [Three Consecutive Odds](https://leetcode.com/problems/three-consecutive-odds)

### Solution :

Method 1 (Greedy, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn three_consecutive_odds(arr: Vec<i32>) -> bool {
        let mut amount_cumulative_odd: u8 = 0;
        for num in arr {
            match num % 2 {
                1 => amount_cumulative_odd += 1,
                0 | _ => amount_cumulative_odd = 0,
            };

            if amount_cumulative_odd == 3 {
                return true
            }
        }

        return false
    }
}
```

### Solution :

Method 1 (Greedy, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def threeConsecutiveOdds(self, arr: List[int]) -> bool:
        amount_cumulative_odd = 0
        for num in arr:
            if num % 2 == 1:
                amount_cumulative_odd += 1
            else:
                amount_cumulative_odd = 0

            if amount_cumulative_odd == 3:
                return True

        return False
```
