![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 884. [Uncommon Words From Two Sentences](https://leetcode.com/problems/uncommon-words-from-two-sentences)

### Solution :

Method 1 (Time Complexity: $O(M+N)$, Space Complexity: $O(M+N)$ (M: number of the elements in `s1`, N: number of the elements in `s2`)) :
```rust
use std::collections::HashMap;

const SPACE: u8 = b' ';
impl Solution {
    pub fn uncommon_from_sentences(s1: String, s2: String) -> Vec<String> {
        let mut counter: HashMap<String, i32> = HashMap::new();
        /* Option 1 */
        Self::assemble_counter(&s1, &mut counter);
        Self::assemble_counter(&s2, &mut counter);
        /* Option 2

        Self::assemble_counter(&(format!("{} {}", s1, s2)), &mut counter);
        */

        let mut result: Vec<String> = Vec::new();
        for (key, value) in counter {
            if value != 1 {
                continue;
            }

            result.push(key);
        }

        return result
    }

    fn assemble_counter(s: &String, counter: &mut HashMap<String, i32>) {
        let length: usize = s.len();
        let mut index_previous: usize = 0;
        let bytes_s = s.as_bytes();
        for index in 0..length {
            if index == length-1 || bytes_s[index+1] == SPACE {
                counter.entry(String::from_utf8(bytes_s[index_previous..=index].to_vec()).unwrap()).and_modify(|value| *value += 1).or_insert(1);
                index_previous = index + 2;
            }
        }
    }
}
```
