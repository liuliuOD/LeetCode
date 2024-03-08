![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Length Of Last Word](https://leetcode.com/problems/length-of-last-word)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn length_of_last_word(s: String) -> i32 {
        s.chars().rev().into_iter().skip_while(|&val| val == ' ').take_while(|&val| val != ' ').collect::<String>().len() as i32
    }
}
```

Method 2 :
```rust
impl Solution {
    pub fn length_of_last_word(s: String) -> i32 {
        let mut spliter = s.split(' ');
        while let Some(temp) = spliter.next_back() {
            match temp.len() as i32 {
                0 => (),
                value => {
                    return value
                },
            }
        }
        0
    }
}
```
