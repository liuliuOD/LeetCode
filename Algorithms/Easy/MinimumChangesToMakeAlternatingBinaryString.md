![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1758. [Minimum Changes To Make Alternating Binary String](https://leetcode.com/problems/minimum-changes-to-make-alternating-binary-string)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn min_operations(s: String) -> i32 {
        let mut leading_0: i32 = 0;
        let mut leading_1: i32 = 0;
        /* Option 1 */
        for (index, ch) in s.chars().enumerate() {
            if (index % 2 == 0 && ch == '1') || (index % 2 == 1 && ch == '0') {
        /* Option 2

        for (index, ascii) in s.bytes().enumerate() {
            if (index % 2 == 0 && ascii == b'1') || (index % 2 == 1 && ascii == b'0') {
        */
                leading_0 += 1;
            } else {
                leading_1 += 1;
            }
        }

        return leading_0.min(leading_1)
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def minOperations(self, s: str) -> int:
        n = len(s)
        # Option 1
        leading_zero = 0
        for index in range(n):
            if (index%2 == 0 and s[index] == '1') or (index%2 == 1 and s[index] == '0'):
                leading_zero += 1

        leading_one = 0
        for index in range(n):
            if (index%2 == 0 and s[index] == '0') or (index%2 == 1 and s[index] == '1'):
                leading_one += 1
        """
        # Option 2

        leading_zero = 0
        leading_one = 0
        for index in range(n):
            if (index%2 == 0 and s[index] == '1') or (index%2 == 1 and s[index] == '0'):
                leading_zero += 1

            if (index%2 == 0 and s[index] == '0') or (index%2 == 1 and s[index] == '1'):
                leading_one += 1
        """

        return min(leading_zero, leading_one)
```