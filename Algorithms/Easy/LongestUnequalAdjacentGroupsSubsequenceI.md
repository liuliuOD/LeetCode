![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2900. [Longest Unequal Adjacent Groups Subsequence I](https://leetcode.com/problems/longest-unequal-adjacent-groups-subsequence-i)

### Solution :

Method 1 (Greedy, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in `words`)) :
```rust
impl Solution {
    pub fn get_longest_subsequence(words: Vec<String>, groups: Vec<i32>) -> Vec<String> {
        let n: usize = words.len();
        let mut current_group: i32 = groups[0];
        let mut result: Vec<String> = Vec::from([words[0].clone()]);
        for index in 1..n {
            if groups[index] == current_group {
                continue;
            }
            current_group = groups[index];
            result.push(words[index].clone());
        }

        return result
    }
}
```
