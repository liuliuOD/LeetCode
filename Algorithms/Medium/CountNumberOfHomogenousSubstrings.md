![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1759. [Count Number Of Homogenous Substrings](https://leetcode.com/problems/count-number-of-homogenous-substrings)

### Solution :

Method 1 :
```rust
const MODULO: i32 = 1_000_000_007;

impl Solution {
    pub fn count_homogenous(s: String) -> i32 {
        let n: usize = s.len();
        let s: Vec<char> = s.chars().collect::<Vec<char>>();
        let mut length: i32 = 1;
        let mut result: i32 = 1;
        for index in 1..n {
            if s[index] == s[index-1] {
                length += 1;
            } else {
                length = 1;
            }

            result = (result + length) % MODULO;
        }

        return result
    }
}
```

### Solution :

Method 1 (Two Pointers, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
MODULO = 1_000_000_007
class Solution:
    def countHomogenous(self, s: str) -> int:
        n = len(s)
        left = right = 0
        result = 0
        while right < n-1:
            right += 1
            if s[left] == s[right]:
                continue

            """
            Homogenous: when there are a string that length is `N` and all of the chars in it are the same. We can find following pattern.

            N= -> Homogenous=
            1  -> 1
            2  -> 1 + 2 = 3
            3  -> 1 + 2 + 3 = 6
            4  -> 1 + 2 + 3 + 4 = 10
            ...
            """
            n_same = right - left
            result += n_same * (n_same+1) // 2 % MODULO
            left = right

        if s[left] == s[right]:
            n_same = right - left + 1
            result += n_same * (n_same+1) // 2 % MODULO

        return result % MODULO
```

Method 2 :
```python
MODULO = 1_000_000_007
class Solution:
    def countHomogenous(self, s: str) -> int:
        n = len(s)
        length = 1
        # Option 1
        result = 1
        for index in range(1, n):
            if s[index] == s[index-1]:
                length += 1
            else:
                length = 1

            result = (result + length) % MODULO

        return result
        """
        # Option 2

        result = 0
        for index in range(1, n):
            if s[index] == s[index-1]:
                length += 1
            else:
                result += length*(length+1)//2 % MODULO
                length = 1

        return (result + length*(length+1)//2) % MODULO
        """
```
