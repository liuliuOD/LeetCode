![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 838. [Push Dominoes](https://leetcode.com/problems/push-dominoes)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the length of `dominoes`)) :
```rust
impl Solution {
    pub fn push_dominoes(dominoes: String) -> String {
        let dominoes: &[u8] = dominoes.as_bytes();
        let n: usize = dominoes.len();
        let mut mapping: Vec<(i32, u8)> = Vec::from([(-1, b'L')]);
        for (index, &domino) in dominoes.iter().enumerate() {
            if domino == b'.' {
                continue;
            }

            mapping.push((index as i32, domino));
        }

        mapping.push((n as i32, b'R'));
        let m: usize = mapping.len();
        let mut result: Vec<u8> = dominoes.to_vec();
        for index in 0..m-1 {
            let (left, ascii_left) = mapping[index];
            let (right, ascii_right) = mapping[index+1];
            if ascii_left == ascii_right {
                for index_current in (left+1) as usize..right as usize {
                    result[index_current] = ascii_left;
                }
            } else if ascii_left > ascii_right {
                // R > L
                for index_current in (left+1)..right {
                    if index_current-left == right-index_current {
                        result[index_current as usize] = b'.';
                    } else if index_current-left < right-index_current {
                        result[index_current as usize] = b'R';
                    } else {
                        result[index_current as usize] = b'L';
                    }
                }
            }
        }

        return String::from_utf8(result).unwrap()
    }
}
```
