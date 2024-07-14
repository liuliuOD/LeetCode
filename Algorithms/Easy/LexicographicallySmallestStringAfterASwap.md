![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3216. [Lexicographically Smallest String After A Swap](https://leetcode.com/problems/lexicographically-smallest-string-after-a-swap)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: length of `s`)) :
```Rust
const BASE: u8 = b'0';

impl Solution {
    pub fn get_smallest_string(s: String) -> String {
        let mut bytes: Vec<u8> = s.as_bytes().to_vec();
        for index in 0..bytes.len()-1 {
            let num_current: u8 = bytes[index] - BASE;
            let num_next: u8 = bytes[index+1] - BASE;
            if num_current%2 == num_next%2 && num_current > num_next {
                bytes.swap(index, index+1);
                break;
            }
        }

        return String::from_utf8_lossy(&bytes).to_string()
    }
}
```

Method 2 (Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: length of `s`)) :
```rust
impl Solution {
    pub fn get_smallest_string(s: String) -> String {
        let mut bytes: Vec<u8> = s.as_bytes().to_vec();
        for index in 0..bytes.len()-1 {
            if bytes[index]&1 == bytes[index+1]&1 && bytes[index] > bytes[index+1] {
                bytes.swap(index, index+1);
                break;
            }
        }

        return String::from_utf8_lossy(&bytes).to_string()
    }
}
```
