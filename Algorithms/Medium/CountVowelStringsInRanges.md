![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2559. [Count Vowel Strings In Ranges](https://leetcode.com/problems/count-vowel-strings-in-ranges)

### Solution :

Method 1 (Prefix Sum, Time Complexity: $O(M+N)$, Space Complexity: $O(N)$ (M: the number of the elements in `queries`, N: the number of the elements in `words`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn vowel_strings(words: Vec<String>, queries: Vec<Vec<i32>>) -> Vec<i32> {
        let vowels: HashSet<char> = HashSet::from(['a', 'e', 'i', 'o', 'u']);
        let n: usize = words.len();
        let mut prefix_sum: Vec<i32> = vec![0; n+1];
        for index in 0..n {
            let chars: Vec<char> = words[index].chars().collect::<Vec<char>>();
            if vowels.contains(&chars[0]) && vowels.contains(chars.last().unwrap()) {
                prefix_sum[index+1] = prefix_sum[index] + 1;
                continue;
            }

            prefix_sum[index+1] = prefix_sum[index];
        }

        let m: usize = queries.len();
        let mut result: Vec<i32> = vec![0; m];
        for (index, query) in queries.into_iter().enumerate() {
            result[index] = prefix_sum[query[1] as usize + 1] - prefix_sum[query[0] as usize];
        }
        return result
    }
}
```
