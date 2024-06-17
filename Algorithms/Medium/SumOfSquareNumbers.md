![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 633. [Sum Of Square Numbers](https://leetcode.com/problems/sum-of-square-numbers)

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(\sqrt{N})$, Space Complexity: $O(1)$) :
```rust
use std::cmp::Ordering;
impl Solution {
    pub fn judge_square_sum(c: i32) -> bool {
        let c: i64 = c as i64;
        let mut left: i64 = 0;
        let mut right: i64 = f64::sqrt(c as f64) as i64;
        while left <= right {
            let temp: i64 = i64::pow(left, 2) + i64::pow(right, 2);

            match temp.cmp(&c) {
                Ordering::Greater => right -= 1,
                Ordering::Less => left += 1,
                Ordering::Equal => {
                    return true
                },
            }
        }

        return false
    }
}
```

### Solution :

Method 1 (Pre-Calculate + Binary Search + Hash Map + Hash Set, Time Complexity: $O(M+Log(N))$ (M: amount of powered elements lower than `c`, N: $5*10^4$), Space Complexity: $O(MAX(N, 5*10^4))$) :
```python
MAPPING: set[int] = set()
CANDIDATES: list[int] = []
for i in range(50000):
    CANDIDATES.append(i**2)
    MAPPING.add(i**2)

class Solution:
    def judgeSquareSum(self, c: int) -> bool:
        index = bisect.bisect_left(CANDIDATES, c)
        for i in range(index+1):
            if c - CANDIDATES[i] in MAPPING:
                return True

        return False
```

Method 2 (Two Pointer, Time Complexity: $O(\sqrt{N})$, Space Complexity: $O(1)$) :
```python
class Solution:
    def judgeSquareSum(self, c: int) -> bool:
        left, right = 0, int(c**0.5) + 1
        while left <= right:
            temp = left**2 + right**2
            if temp == c:
                return True
            elif temp < c:
                left += 1
            elif temp > c:
                right -= 1

        return False
```
