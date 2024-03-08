![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 168. [Excel Sheet Column Title](https://leetcode.com/problems/excel-sheet-column-title)

### Solution :

Method 1 (Brute Force) :
```rust
impl Solution {
    pub fn convert_to_title(column_number: i32) -> String {
        let mut column_number = column_number;
        let mut result: String = String::new();
        while column_number > 0 {
            column_number -= 1;
            result.insert(0, (b'A' + (column_number%26) as u8) as char);
            column_number /= 26;
        }
        return result
    }
}
```

### Solution :

Method 1 (Brute Force) :
```python
BASE = ord('A')
ALPHA_AMOUNT = 26
class Solution:
    def convertToTitle(self, column_number: int) -> str:
        result = deque()
        while column_number:
            column_number -= 1
            offset = column_number % ALPHA_AMOUNT
            result.appendleft(chr(BASE+offset))
            column_number //= ALPHA_AMOUNT

        return ''.join(result)
```
