![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1903. [Largest Odd Number In String](https://leetcode.com/problems/largest-odd-number-in-string)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn largest_odd_number(num: String) -> String {
        let n: usize = num.len();
        let mut index: usize = n - 1;
        while index < n {
            if (num.as_bytes()[index] - b'0') % 2 == 1 {
                break;
            }

            index -= 1;
        }

        return match index < n {
            true => num[..=index].to_string(),
            _ => "".to_string(),
        }
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def largestOddNumber(self, num: str) -> str:
        n = len(num)
        index = n - 1
        while index >= 0:
            # Option 1
            if (ord(num[index])-ord("0"))%2 == 1:
            """
            # Option 2

            if int(num[index])%2 == 1:
            """
                break

            index -= 1

        return num[:index+1] if index >= 0 else ""
```
