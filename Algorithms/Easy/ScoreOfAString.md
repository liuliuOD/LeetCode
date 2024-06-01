![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 3110. [Score Of A String](https://leetcode.com/problems/score-of-a-string)

### Solution :

Method 1 (Built-In Method, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn score_of_string(s: String) -> i32 {
        /* Option 1 */
        let s_bytes: Vec<u8> = s.into_bytes();
        /* Option 2

        let s_bytes: &[u8] = s.as_bytes();
        */
        return (0..s_bytes.len()-1).fold(0, |result, index| result + (s_bytes[index] as i32 - s_bytes[index+1] as i32).abs())
    }
}
```

Method 2 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn score_of_string(s: String) -> i32 {
        let s_bytes: &[u8] = s.as_bytes();
        let mut result: i32 = 0;
        for index in 0..s_bytes.len()-1 {
            result += (s_bytes[index] as i32 - s_bytes[index+1] as i32).abs();
        }

        return result
    }
}
```

### Solution :

Method 1 (Built-In Method, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def scoreOfString(self, s: str) -> int:
        return reduce(lambda result, index: result + abs(ord(s[index])-ord(s[index+1])), range(len(s)-1), 0)
```

Method 2 (Built-In Method, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def scoreOfString(self, s: str) -> int:
        return sum(abs(ord(a)-ord(b)) for a, b in pairwise(s))
```
