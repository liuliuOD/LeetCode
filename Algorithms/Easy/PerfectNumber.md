![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 905. [Perfect Number](https://leetcode.com/problems/perfect-number)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn check_perfect_number(num: i32) -> bool {
        let mut sum_factors: i32 = 0;
        for candidate in 1..=num/2 {
            if num % candidate == 0 {
                sum_factors += candidate;
            }
        }

        return sum_factors == num
    }
}
```

Method 2 (Time Complexity: $O(\sqrt{N})$, Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn check_perfect_number(num: i32) -> bool {
        if num == 1 {
            return false
        }

        let mut sum_factors: i32 = -num;
        for candidate in 1..=((num as f32).sqrt() as i32) {
            if num % candidate == 0 {
                sum_factors += candidate + num / candidate;
            }
        }

        return sum_factors == num
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(\sqrt{N})$, Space Complexity: $O(1)$) :
```python
class Solution:
    def checkPerfectNumber(self, num: int) -> bool:
        if num == 1:
            return False

        divisor_sum = -num
        for divisor in range(1, int(num**0.5) + 1):
            if num % divisor == 0:
                divisor_sum += divisor + num // divisor

        return num == divisor_sum
```

Method 2 ([Euclid-Euler Theorem](https://leetcode.com/problems/perfect-number/editorial), Time Complexity: $O(1)$, Space Complexity: $O(1)$) :
```python
PERFECT_NUMS: set[int] = set((2**p - 1) * 2**(p - 1) for p in [2, 3, 5, 7, 13])

class Solution:
    def checkPerfectNumber(self, num: int) -> bool:
        return num in PERFECT_NUMS
```
