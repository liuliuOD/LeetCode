![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 781. [Rabbits In Forest](https://leetcode.com/problems/rabbits-in-forest)

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of the elements in `answers`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn num_rabbits(answers: Vec<i32>) -> i32 {
        let mut counter: HashMap<i32, i32> = HashMap::new();
        for num in &answers {
            counter.entry(*num).and_modify(|amount| *amount += 1).or_insert(1);
        }

        let mut result: i32 = 0;
        for key in counter.keys() {
            let amount_group: i32 = *counter.get(key).unwrap() / (key+1);
            result += amount_group*(key+1);

            let amount_remaining: i32 = *counter.get(key).unwrap() % (key+1);
            if amount_remaining > 0 {
                result += key + 1;
            }
        }

        return result
    }
}
```
