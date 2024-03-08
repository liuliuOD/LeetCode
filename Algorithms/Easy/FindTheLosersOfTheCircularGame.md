![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2682. [Find The Losers Of The Circular Game](https://leetcode.com/problems/find-the-losers-of-the-circular-game)

### Solution :

Method 1 (In weekly contest 345) :
```rust
impl Solution {
    pub fn circular_game_losers(n: i32, k: i32) -> Vec<i32> {
        let n = n as usize;
        let k = k as usize;
        let mut people = vec![false; n];
        let mut count = 0;
        let mut ite = 0;
        while people[count] == false {
            people[count] = true;
            ite += 1;
            count = (count + ite*k) % n;
        }

        let mut result = vec![];
        for (index, person) in people.iter().enumerate() {
            if !person {
                result.push((index + 1) as i32);
            }
        }
        
        result
    }
}
```
