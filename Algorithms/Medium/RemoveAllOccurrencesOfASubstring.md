![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1910. [Remove All Occurrences Of A Substring](https://leetcode.com/problems/remove-all-occurrences-of-a-substring)

### Solution :

Method 1 (Stack, Time Complexity: $O(M*N)$, Space Complexity: $O(M+N)$ (M: the length of `part`, N: the length of `s`)) :
```rust
impl Solution {
    pub fn remove_occurrences(s: String, part: String) -> String {
        let s_bytes: Vec<u8> = s.into_bytes();
        let part_bytes: Vec<u8> = part.into_bytes();
        let m: usize = part_bytes.len();
        let mut stack: Vec<u8> = Vec::new();
        for ascii in s_bytes {
            stack.push(ascii);
            if stack.len() < part_bytes.len() {
                continue;
            }

            let n: usize = stack.len();
            let mut index_stack: usize = n;
            for index_part in (0..m).rev() {
                if stack[index_stack-1] != part_bytes[index_part] {
                    break;
                }

                index_stack -= 1;
            }
            if (n-index_stack) == m {
                stack.truncate(index_stack);
            }
        }

        return String::from_utf8(stack).unwrap()
    }
}
```
