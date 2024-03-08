![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Determine The Winner Of A Bowling Game](https://leetcode.com/problems/determine-the-winner-of-a-bowling-game)

### Solution :

Method 1 (In weekly contest 343) :
```rust
use std::cmp::Ordering;
impl Solution {
    pub fn is_winner(player1: Vec<i32>, player2: Vec<i32>) -> i32 {
        let mut A = 0;
        let mut B = 0;
        for i in 0..player1.len() {
            if i == 0 {
                A += player1[i];
                B += player2[i];
            }
            else if i == 1 {
                match player1[i-1] == 10 {
                    true => A += player1[i] * 2,
                    false => A += player1[i],
                }
                match player2[i-1] == 10 {
                    true => B += player2[i] * 2,
                    false => B += player2[i],
                }
            }
            else {
                match player1[i-1] == 10 || player1[i-2] == 10 {
                    true => A += player1[i] * 2,
                    false => A += player1[i],
                }
                match player2[i-1] == 10 || player2[i-2] == 10 {
                    true => B += player2[i] * 2,
                    false => B += player2[i],
                }
            }
        }
        
        match A.cmp(&B) {
            Ordering::Equal => 0,
            Ordering::Less => 2,
            Ordering::Greater => 1,
        }
    }
}
```
