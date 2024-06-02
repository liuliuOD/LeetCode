![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 344. [Reverse String](https://leetcode.com/problems/reverse-string)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn reverse_string(mut s: &mut Vec<char>) {
        let n: usize = s.len();
        for index in 0..(n/2) {
            s.swap(index, n-index-1);
        }
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        n = len(s)
        for index in range(n//2):
            index_correspond = n - index - 1
            s[index], s[index_correspond] = s[index_correspond], s[index]
```

Method 2 (Built-In Method, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def reverseString(self, s: List[str]) -> None:
        """
        Do not return anything, modify s in-place instead.
        """
        # Option 1
        s[:] = s[::-1]
        """
        # Option 2

        s.reverse()
        """
```
