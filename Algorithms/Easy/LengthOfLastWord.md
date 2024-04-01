![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
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

### Solution :

Method 1 (Built-In Library, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```go
import "strings"

func lengthOfLastWord(s string) int {
    split := strings.Split(strings.TrimSpace(s), " ")

    return len(split[len(split)-1])
}
```

Method 2 (Built-In Library, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```go
func lengthOfLastWord(s string) int {
    result := 0
    for index := len(s)-1; index >= 0; index-- {
        if s[index] != ' ' {
            result++
        } else if result > 0 {
            break
        }
    }

    return result
}
```
