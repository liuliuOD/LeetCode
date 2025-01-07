![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-JAVA](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk)
---

## 1408. [String Matching In An Array](https://leetcode.com/problems/string-matching-in-an-array)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$ (N: the number of the elements in `words`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn string_matching(mut words: Vec<String>) -> Vec<String> {
        let n: usize = words.len();
        words.sort_by_key(|item| item.len());
        let mut substrings: HashSet<String> = HashSet::new();
        for index in 0..n {
            for index_another in index+1..n {
                if words[index_another].contains(&words[index]) {
                    substrings.insert(words[index].clone());
                    break;
                }
            }
        }

        return Vec::from_iter(substrings)
    }
}
```

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$ (N: the number of the elements in `words`)) :
```java
class Solution {
    public List<String> stringMatching(String[] words) {
        int n = words.length;
        List<String> result = new ArrayList<>();
        for (int index=0; index<n; index++) {
            for (int index_next=0; index_next<n; index_next++) {
                if (index != index_next && words[index_next].contains(words[index])) {
                    result.add(words[index]);
                    break;
                }
            }
        }

        return result;
    }
}
```
