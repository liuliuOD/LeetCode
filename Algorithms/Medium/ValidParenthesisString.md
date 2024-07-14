![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 678. [Valid Parenthesis String](https://leetcode.com/problems/valid-parenthesis-string)

### Solution :

Method 1 (Two Direction, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: length of `s`)) :
```rust
impl Solution {
    pub fn check_valid_string(s: String) -> bool {
        let n: usize = s.len();
        let chars: Vec<char> = s.chars().into_iter().collect();
        let mut amount_left: i32 = 0;
        for index in 0..n {
            match chars[index] {
                '(' | '*' => amount_left += 1,
                ')' | _ => amount_left -= 1,
            };

            if amount_left < 0 {
                return false
            }
        }

        let mut amount_right: i32 = 0;
        for index in (0..n).rev() {
            match chars[index] {
                ')' | '*' => amount_right += 1,
                '(' | _ => amount_right -= 1,
            };

            if amount_right < 0 {
                return false
            }
        }

        return true
    }
}
```

Method 2 (Two Direction, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: length of `s`)) :
```rust
impl Solution {
    pub fn check_valid_string(s: String) -> bool {
        let mut amount_left: i32 = 0;
        for character in s.chars() {
            match character {
                '(' | '*' => amount_left += 1,
                ')' | _ => amount_left -= 1,
            };

            if amount_left < 0 {
                return false
            }
        }

        let mut amount_right: i32 = 0;
        for character in s.chars().rev() {
            match character {
                ')' | '*' => amount_right += 1,
                '(' | _ => amount_right -= 1,
            };

            if amount_right < 0 {
                return false
            }
        }

        return true
    }
}
```

### Solution :

Method 1 (Two Direction, Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: length of `s`)) :
```python
class Solution:
    def checkValidString(self, s: str) -> bool:
        depth_a = 0
        for char in s:
            if char in ['*', '(']:
                depth_a += 1
            elif char == ')':
                depth_a -= 1

            if depth_a < 0:
                return False

        depth_b = 0
        for char in s[::-1]:
            if char == '(':
                depth_b += 1
            elif char in ['*', ')']:
                depth_b -= 1

            if depth_b > 0:
                return False

        return True
```
