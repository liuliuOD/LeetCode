![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1704. [Determine If String Halves Are Alike](https://leetcode.com/problems/determine-if-string-halves-are-alike)

### Solution :

Method 1 :
```rust
use std::collections::HashSet;
impl Solution {
    pub fn halves_are_alike(s: String) -> bool {
        /* Option 1 */
        let BASE: HashSet<u8> = HashSet::from([b'a', b'e', b'i', b'o', b'u', b'A', b'E', b'I', b'O', b'U']);
        /* Option 2
        
        let BASE: [u8; 10] = [b'a', b'e', b'i', b'o', b'u', b'A', b'E', b'I', b'O', b'U'];
        */
        let n: usize = s.len();
        let mut amount: i32 = 0;
        for (index, ascii) in s.bytes().enumerate() {
            if ! BASE.contains(&ascii) {
                continue;
            }

            if index < n/2 {
                amount += 1;
            } else {
                amount -= 1;
            }
        }

        return amount == 0
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def halvesAreAlike(self, s: str) -> bool:
        n = len(s)
        amount = 0
        for index in range(n):
            if s[index].lower() not in ['a', 'e', 'i', 'o', 'u']:
                continue

            # left half
            if index < n // 2:
                amount += 1
            # right half
            else:
                amount -= 1

        return amount == 0
```
