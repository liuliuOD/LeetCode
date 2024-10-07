![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2696. [Minimum String Length After Removing Substrings](https://leetcode.com/problems/minimum-string-length-after-removing-substrings)

### Solution :

Method 1 (Stack, Time Complexity: $O(N)$, Space Complexity: $O(N)$, (N: the length of `s`)) :
```rust
const A: u8 = b'A';
const B: u8 = b'B';
const C: u8 = b'C';
const D: u8 = b'D';

impl Solution {
    pub fn min_length(s: String) -> i32 {
        let mut stack: Vec<u8> = Vec::new();
        for ascii in s.bytes() {
            match ascii {
                B => {
                    if stack.len() > 0 && *stack.last().unwrap() == A {
                        stack.pop();
                    } else {
                        stack.push(ascii);
                    }
                },
                D => {
                    if stack.len() > 0 && *stack.last().unwrap() == C {
                        stack.pop();
                    } else {
                        stack.push(ascii);
                    }
                },
                _ => {
                    stack.push(ascii);
                },
            }
        }

        return stack.len() as i32
    }
}
```

### Solution :

Method 1 (In weekly contest 346) :
```python
class Solution:
    def minLength(self, s: str) -> int:
        return self.remove(s)
    def remove(self, s: str) -> int:
        s_new = re.sub(r'(AB|CD)', '', s)
        if len(s) == len(s_new):
            return len(s)
        return self.remove(s_new)
```
