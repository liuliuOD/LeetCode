![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Find The Index Of The First Occurrence In A String](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn str_str(haystack: String, needle: String) -> i32 {
        match haystack.find(&needle) {
            Some(index) => index as i32,
            None => -1,
        }
    }
}
```

Method 2 :
```rust
impl Solution {
    pub fn str_str(haystack: String, needle: String) -> i32 {
        let h_length = haystack.len();
        let n_length = needle.len();

        if n_length == 0 {
            return 0
        } else if h_length < n_length {
            return -1
        }

        for i in 0..=(h_length - n_length) {
            if haystack[i..(i + n_length)] == needle {
                return i as i32
            }
        }

        -1
    }
}
```
