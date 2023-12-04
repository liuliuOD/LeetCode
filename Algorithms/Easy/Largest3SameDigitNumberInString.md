![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2264. [Largest 3-Same-Digit Number In String](https://leetcode.com/problems/largest-3-same-digit-number-in-string)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn largest_good_integer(num: String) -> String {
        let num_chars: Vec<char> = num.chars().collect();
        let mut maximum: u8 = 0;
        for index in 2..num_chars.len() {
            if num_chars[index-2] == num_chars[index-1] && num_chars[index-1] == num_chars[index] {
                maximum = maximum.max(num_chars[index] as u8);
            }
        }

        return match maximum {
            0 => "".to_string(),
            _ => String::from_utf8(vec![maximum, maximum, maximum]).unwrap(),
        }
    }
}
```

Method 2 :
```rust
impl Solution {
    pub fn largest_good_integer(num: String) -> String {
        let num_chars: Vec<u8> = num.as_bytes().to_vec();
        let mut maximum: u8 = 0;
        for index in 2..num_chars.len() {
            if num_chars[index-2] == num_chars[index-1] && num_chars[index-1] == num_chars[index] {
                maximum = maximum.max(num_chars[index]);
            }
        }

        return match maximum {
            0 => "".to_string(),
            /* Option 1 */
            _ => String::from_utf8(vec![maximum, maximum, maximum]).unwrap(),
            /* Option 2

            _ => String::from_utf8(vec![maximum; 3]).unwrap(),
            */
            /* Option 3

            _ => std::str::from_utf8(&[maximum, maximum, maximum]).unwrap().to_string(),
            */
            /* Option 4

            _ => std::str::from_utf8(&[maximum; 3]).unwrap().to_string(),
            */
        }
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def largestGoodInteger(self, num: str) -> str:
        n = len(num)
        result = ""
        for index in range(2, n):
            if num[index-2] == num[index-1] == num[index]:
                if result == "" or num[index] > result[0]:
                    result = num[index] * 3

        return result
```
