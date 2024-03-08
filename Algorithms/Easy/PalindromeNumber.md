![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Palindrome Number](https://leetcode.com/problems/palindrome-number)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn is_palindrome(x: i32) -> bool {
        x.to_string().chars().rev().collect::<String>() == x.to_string()
    }
}
```

Method 2 :
```rust
impl Solution {
    pub fn is_palindrome(x: i32) -> bool {
        x.to_string().chars().rev().collect::<String>().eq(&x.to_string())
    }
}
```

Method 3 :
```rust
impl Solution {
    pub fn is_palindrome(x: i32) -> bool {
        if x < 0 {
            return false
        }

        x.to_string().chars().rev().collect::<String>().eq(&x.to_string())
    }
}
```

Method 4 :
```rust
impl Solution {
    pub fn is_palindrome(x: i32) -> bool {
        if x < 0 {
            return false
        }

        x.to_string().chars().rev().collect::<String>() == x.to_string()
    }
}
```

Method 5 :
```rust
impl Solution {
    pub fn is_palindrome(x: i32) -> bool {
        let bytes_x = x.to_string().into_bytes();
        let mut reverse_bytes_x = bytes_x.to_owned();
        reverse_bytes_x.reverse();

        reverse_bytes_x == bytes_x
    }
}
```

Method 6 (nth() iterately fetch item) :
```rust
impl Solution {
    pub fn is_palindrome(x: i32) -> bool {
        let string_x = x.to_string();
        let mut i = 0;
        let mut j = string_x.len() - 1;
        while(i < j) {
            if (string_x.chars().nth(i) != string_x.chars().nth(j)) {
                return false
            }

            i += 1;
            j -= 1;
        }

        true
    }
}
```

Method 7 (nth() iterately fetch item) :
```rust
impl Solution {
    pub fn is_palindrome(x: i32) -> bool {
        if x < 0 {
            return false
        }

        let string_x = x.to_string();
        let mut i = 0;
        let mut j = string_x.len() - 1;
        while(i < j) {
            if (string_x.chars().nth(i) != string_x.chars().nth(j)) {
                return false
            }

            i += 1;
            j -= 1;
        }

        true
    }
}
```
