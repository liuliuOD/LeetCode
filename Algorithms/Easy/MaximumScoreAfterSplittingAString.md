![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1422. [Maximum Score After Splitting A String](https://leetcode.com/problems/maximum-score-after-splitting-a-string)

### Solution :

Method 1 :
```rust
use std::str::Chars;

impl Solution {
    pub fn max_score(s: String) -> i32 {
        let mut right: i32 = 0;
        for ch in s.chars() {
            if ch == '1' {
                right += 1;
            }
        }

        let mut chars: Chars = s.chars();
        let mut left: i32 = 0;
        let mut result: i32 = 0;
        for index in 0..s.len()-1 {
            let ch: char = chars.next().unwrap();
            match ch { 
                '0' => left += 1,
                _ => right -= 1,
            };

            result = result.max(left + right);
        }

        return result
    }
}
```

Method 2 (Time Complexity: $(N)$, Space Complexity: $O(1)$ (N: the length of `s`)) :
```rust
const BASE: u8 = b'0';

impl Solution {
    pub fn max_score(s: String) -> i32 {
        let s_bytes: &[u8] = s.as_bytes();
        let mut amount_0: i32 = 0;
        let mut amount_1: i32 = s_bytes.iter().filter(|ascii| *ascii-BASE == 1).count() as i32;
        let mut result: i32 = 0;
        for ascii in s_bytes.into_iter().take(s_bytes.len()-1) {
            if ascii-BASE == 0 {
                amount_0 += 1;
            } else {
                amount_1 -= 1;
            }

            result = i32::max(result, amount_0+amount_1);
        }

        return result
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def maxScore(self, s: str) -> int:
        counter = Counter(s)
        left = 0
        result = 0
        for index in range(len(s)-1):
            char = s[index]
            if char == '0':
                left += 1

            counter[char] -= 1
            result = max(result, left + counter["1"])

        return result
```

Method 2 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def maxScore(self, s: str) -> int:
        left = 0
        # Option 1
        right = sum(map(lambda char: int(char), s))
        """
        # Option 2

        right = s.count('1')
        """
        result = 0
        for index in range(len(s)-1):
            if s[index] == '0':
                left += 1
            else:
                right -= 1

            result = max(result, left+right)

        return result
```

Method 3 (Time Complexity: $O(N^2)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def maxScore(self, s: str) -> int:
        result = 0
        for index in range(len(s)-1):
            result = max(result, s[:index+1].count('0') + s[index+1:].count('1'))

        return result
```
