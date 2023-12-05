![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1688. [Count Of Matches In Tournament](https://leetcode.com/problems/count-of-matches-in-tournament)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn number_of_matches(n: i32) -> i32 {
        return n - 1
    }
}
```

Method 2 :
```rust
impl Solution {
    pub fn number_of_matches(mut n: i32) -> i32 {
        let mut result: i32 = 0;
        while n > 1 {
            result += n / 2;
            match n % 2 {
                0 => n /= 2,
                _ => n = n/2 + 1,
            }
        }

        return result
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(Log(N))$, Space Complexity: $O(1)$) :
```python
class Solution:
    def numberOfMatches(self, n: int) -> int:
        result = 0
        while n > 1:
            result += n // 2
            if n % 2 == 0:
                n //= 2
            else:
                n = n//2 + 1

        return result
```

Method 2 (Time Complexity: $O(1)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def numberOfMatches(self, n: int) -> int:
        """
        Because for each match, a loser is generated.
        Finally, there is only one winner.
        That is, there are `n-1` losers generated.
        """
        return n - 1
```
