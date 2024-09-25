![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2416. [Sum Of Prefix Scores Of Strings](https://leetcode.com/problems/sum-of-prefix-scores-of-strings)

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N*K)$, Space Complexity: $O(N*K)$, ERROR: "Time Limit Exceeded" (35/38)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn sum_prefix_scores(words: Vec<String>) -> Vec<i32> {
        let mut mapping: HashMap<String, i32> = HashMap::new();
        for word in words.iter() {
            for length in 1..=word.len() {
                mapping.entry(word[0..length].to_string()).and_modify(|value| *value += 1).or_insert(1);
            }
        }

        let mut result: Vec<i32> = Vec::new();
        for word in words.iter() {
            let mut score: i32 = 0;
            for length in 1..=word.len() {
                score += mapping[&word[0..length].to_string()];
            }

            result.push(score);
        }

        return result
    }
}
```

Method 2 (DFS, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(Log(N))$, ERROR: "Time Limit Exceeded" (41/69)) :
```rust

```
