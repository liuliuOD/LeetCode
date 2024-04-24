![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1201. [Ugly Number III](https://leetcode.com/problems/ugly-number-iii)

### Solution :

Method 1 (Binary Search, Time Complexity: $O(Log(N))$ (N: 2*10^9), Space Complexity: $O(1)$) :
```python
class Solution:
    def nthUglyNumber(self, n: int, a: int, b: int, c: int) -> int:
        left, right = 1, 2_000_000_000
        while left <= right:
            middle = left + (right - left) // 2

            amount = middle // a + middle // b + middle // c - middle // self.get_lcm(a, b) - middle // self.get_lcm(b, c) - middle // self.get_lcm(a, c) + middle // self.get_lcm(self.get_lcm(a, b), c)
            if amount < n:
                left = middle + 1
            else:
                right = middle - 1

        return left

    def get_gcd(self, a: int, b: int) -> int:
        if a == 0:
            return b
        return self.get_gcd(b%a, a)

    def get_lcm(self, a: int, b: int) -> int:
        return a * b // self.get_gcd(a, b)
```
