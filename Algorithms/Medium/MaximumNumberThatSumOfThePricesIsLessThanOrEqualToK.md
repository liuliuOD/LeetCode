![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 3007. [Maximum Number That Sum Of The Prices Is Less Than Or Equal To K](https://leetcode.com/problems/maximum-number-that-sum-of-the-prices-is-less-than-or-equal-to-k)

### Solution :

Method 1 (Binary Search) :
```python
class Solution:
    def findMaximumNumber(self, k: int, x: int) -> int:
        left = 1
        right = 1_000_000_000_000_000
        while left <= right:
            middle = left + (right - left)//2
            prices = self.getPrices(middle, x)
            if prices <= k:
                left = middle + 1
            else:
                right = middle - 1

        return right

    def getPrices(self, num: int, x: int) -> int:
        prices = 0
        amount_bits = len(bin(num)) - 2

        num += 1
        while amount_bits:
            if amount_bits % x == 0:
                power_bit = 1 << amount_bits
                power_bit_minus_1 = 1 << (amount_bits-1)
                prices += (num >> amount_bits) * power_bit_minus_1 + max(0, num % power_bit - power_bit_minus_1)

            amount_bits -= 1

        return prices
```

Method 2 (Binary Search) :
```python
class Solution:
    def findMaximumNumber(self, k: int, x: int) -> int:
        return bisect.bisect_right(range((1<<63) - 1), k, key=lambda value: self.getPrices(value, x)) - 2

    def getPrices(self, num: int, x: int) -> int:
        result = 0
        for index in range(x-1, 64, x):
            num_ = num % (1<<(index+1))
            result += ((num-num_) >> 1) + max(0, num_ - (1<<index))

        return result
```
