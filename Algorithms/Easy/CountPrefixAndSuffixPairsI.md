![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3042. [Count Prefix And Suffix Pairs I](https://leetcode.com/problems/count-prefix-and-suffix-pairs-i)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N^2)$, Space Complexity: $O(1)$ (N: the number of the elements in `words`)) :
```rust
impl Solution {
    pub fn count_prefix_suffix_pairs(words: Vec<String>) -> i32 {
        let n: usize = words.len();
        let mut result: i32 = 0;
        for index_start in 0..n {
            for index_end in index_start+1..n {
                if words[index_end].starts_with(&words[index_start]) && words[index_end].ends_with(&words[index_start]) {
                    result += 1;
                }
            }
        }

        return result
    }
}
```
