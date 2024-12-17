![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2182. [Construct String With Repeat Limit](https://leetcode.com/problems/construct-string-with-repeat-limit)

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the length of `s`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn repeat_limited_string(s: String, repeat_limit: i32) -> String {
        let mut result: Vec<char> = s.clone().chars().collect::<Vec<char>>();
        let n: usize = result.len();
        result.sort();
        result.reverse();
        let mut mapping: HashMap<char, usize> = HashMap::new();
        for index in 0..n {
            mapping.entry(result[index]).or_insert(index);
        }

        let mut amount: i32 = 1;
        for index in 1..n {
            if result[index] == result[index-1] {
                amount += 1;
            } else {
                amount = 1;
            }

            if amount <= repeat_limit {
                continue;
            }

            let char_current: char = result[index];
            for offset in 1..=(char_current as u8)-b'a' {
                let char_previous: char = (char_current as u8 - offset) as char;
                if mapping.contains_key(&char_previous) {
                    let index_previous: usize = *mapping.get(&char_previous).unwrap();
                    result.swap(index, index_previous);

                    if index_previous < n-1 && result[index_previous+1] == char_previous {
                        mapping.entry(char_previous).and_modify(|index| *index += 1);
                    } else {
                        mapping.remove(&char_previous);
                    }

                    break;
                }
            }

            if result[index] == char_current {
                result = result[0..index].to_vec();
                break;
            }
            amount = 1;
        }

        return result.into_iter().collect::<String>()
    }
}
```

Method 2 (Array, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the length of `s`)) :
```rust
const BASE: u8 = b'a';

impl Solution {
    pub fn repeat_limited_string(s: String, repeat_limit: i32) -> String {
        let mut counter: [i32; 26] = [0; 26];
        for ascii in s.bytes() {
            counter[(ascii-BASE) as usize] += 1;
        }

        let mut result: Vec<char> = Vec::new();
        for index in (0..26).rev() {
            let mut index_previous: usize = index - 1;
            let mut amount: i32 = 0;
            while counter[index] > 0 {
                if amount < repeat_limit {
                    result.push((index as u8 + BASE) as char);
                    counter[index] -= 1;
                    amount += 1;
                    continue;
                }

                if index_previous >= 26 {
                    break;
                }

                while index_previous > 0 && counter[index_previous] == 0 {
                    index_previous -= 1;
                }

                if counter[index_previous] == 0 {
                    break;
                }
                counter[index_previous] -= 1;
                result.push((index_previous as u8 + BASE) as char);
                amount = 0;
            }
        }

        return result.into_iter().collect::<String>()
    }
}
```
