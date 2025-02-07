![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3160. [Find The Number Of Distinct Colors Among The Balls](https://leetcode.com/problems/find-the-number-of-distinct-colors-among-the-balls)

### Solution :

Method 1 (Hash Map, Time Complexity: $O(M)$, Space Complexity: $O(N)$ (M: the number of elements in `queries`, N: the value of `limit`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn query_results(limit: i32, queries: Vec<Vec<i32>>) -> Vec<i32> {
        let mut groups: HashMap<i32, i32> = HashMap::new();
        let mut colors: HashMap<i32, i32> = HashMap::new();
        let mut result: Vec<i32> = Vec::new();
        for query in queries {
            let ball: i32 = query[0];
            let color: i32 = query[1];
            if colors.contains_key(&ball) {
                let color_old: &i32 = colors.get(&ball).unwrap();
                groups.entry(*color_old).and_modify(|amount| *amount -= 1);
                if *groups.get(color_old).unwrap() <= 0 {
                    groups.remove(color_old);
                }
            }

            *colors.entry(ball).or_default() = color;
            *groups.entry(color).or_default() += 1;
            result.push(groups.len() as i32);
        }

        return result
    }
}
```
