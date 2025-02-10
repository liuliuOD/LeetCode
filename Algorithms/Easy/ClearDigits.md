![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3174. [Clear Digits](https://leetcode.com/problems/clear-digits)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the length of `s`)) :
```rust
impl Solution {
    pub fn clear_digits(s: String) -> String {
        let mut result: String = "".to_string();
        for character in s.chars() {
            if character.is_ascii_digit() {
                result.pop();
                continue;
            }

            /* Option 1 */
            result.push_str(character.encode_utf8(&mut [0]));
            /* Option 2

            result.push(character);
            */
        }

        return result
    }
}
```

Method 2 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the length of `s`)) :
```rust
impl Solution {
    pub fn clear_digits(s: String) -> String {
        let n: usize = s.len();
        let mut index_pointer: usize = 0;
        let mut result: Vec<u8> = s.into_bytes();
        for index in 0..n {
            if b'0' <= result[index] && result[index] <= b'9' {
                index_pointer -= 1;
                continue;
            }

            result[index_pointer] = result[index];
            index_pointer += 1;
        }

        return String::from_utf8(result[0..index_pointer].to_vec()).unwrap()
    }
}
```
