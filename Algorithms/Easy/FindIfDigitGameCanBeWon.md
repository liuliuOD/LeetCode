![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3232. [Find If Digit Game Can Be Won](https://leetcode.com/problems/find-if-digit-game-can-be-won)

### Solution :

Method 1 (Greedy, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn can_alice_win(nums: Vec<i32>) -> bool {
        let mut sum_single: i32 = 0;
        let mut sum_double: i32 = 0;
        for num in nums {
            match num >= 10 {
                true => sum_double += num,
                false => sum_single += num,
            }
        }

        return sum_single != sum_double
    }
}
```
