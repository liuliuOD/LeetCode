![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1371. [Find The Longest Substring Containing Vowels In Even Counts](https://leetcode.com/problems/find-the-longest-substring-containing-vowels-in-even-counts)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of the characters in `s`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn find_the_longest_substring(s: String) -> i32 {
        let n: usize = s.len();
        let mut prefix_xor: Vec<u8> = Vec::with_capacity(n+1);
        prefix_xor.push(0);
        for character in s.as_bytes() {
            match character {
                b'a' => prefix_xor.push(prefix_xor.last().unwrap() ^ 1 << 4),
                b'e' => prefix_xor.push(prefix_xor.last().unwrap() ^ 1 << 3),
                b'i' => prefix_xor.push(prefix_xor.last().unwrap() ^ 1 << 2),
                b'o' => prefix_xor.push(prefix_xor.last().unwrap() ^ 1 << 1),
                b'u' => prefix_xor.push(prefix_xor.last().unwrap() ^ 1 << 0),
                _ => prefix_xor.push(*prefix_xor.last().unwrap()),
            };
        }

        let mut result: i32 = 0;
        let mut mapping: HashMap<usize, usize> = HashMap::new();
        for index in 0..prefix_xor.len() {
            mapping.entry(prefix_xor[index] as usize).and_modify(|value| result = i32::max(result, (index-*value) as i32)).or_insert(index);
        }

        return result
    }
}
```

Method 2 (Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of the characters in `s`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn find_the_longest_substring(s: String) -> i32 {
        let n: usize = s.len();
        let mut prefix_xor: u8 = 0;
        let mut mapping: HashMap<u8, i32> = HashMap::from([(0, -1)]);
        let mut result: i32 = 0;
        for (index, &character) in s.as_bytes().into_iter().enumerate() {
            match character {
                b'a' => prefix_xor ^= 1 << 4,
                b'e' => prefix_xor ^= 1 << 3,
                b'i' => prefix_xor ^= 1 << 2,
                b'o' => prefix_xor ^= 1 << 1,
                b'u' => prefix_xor ^= 1 << 0,
                _ => {},
            };

            mapping.entry(prefix_xor).and_modify(|value| result = i32::max(result, index as i32 - *value)).or_insert(index as i32);
        }

        return result
    }
}
```

Method 3 (Array in the Stack, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of the characters in `s`)) :
```rust
use std::collections::HashMap;

impl Solution {
    pub fn find_the_longest_substring(s: String) -> i32 {
        let n: usize = s.len();
        let mut prefix_xor: usize = 0;
        let mut mapping: [i32; 1 << 5] = [-2; 1 << 5];
        mapping[0] = -1;
        let mut result: i32 = 0;
        for (index, character) in s.chars().enumerate() {
            match character {
                'a' => prefix_xor ^= 1 << 4,
                'e' => prefix_xor ^= 1 << 3,
                'i' => prefix_xor ^= 1 << 2,
                'o' => prefix_xor ^= 1 << 1,
                'u' => prefix_xor ^= 1 << 0,
                _ => {},
            };

            if mapping[prefix_xor] >= -1 {
                result = i32::max(result, index as i32 - mapping[prefix_xor]);
            } else {
                mapping[prefix_xor] = index as i32;
            }
        }

        return result
    }
}
```
