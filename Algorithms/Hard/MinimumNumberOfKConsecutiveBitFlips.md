![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 995. [Minimum Number Of K Consecutive Bit Flips](https://leetcode.com/problems/minimum-number-of-k-consecutive-bit-flips)

### Solution :

Method 1 (Dynamic Programming, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minKBitFlips(self, nums: List[int], k: int) -> int:
        n = len(nums)
        dp = [False] * n
        amount_flips = 0
        result = 0
        for index in range(n):
            if index >= k and dp[index-k]:
                amount_flips -= 1

            if amount_flips % 2 != nums[index]:
                continue

            if index+k-1 >= n:
                result = -1
                break

            dp[index] = True
            result += 1
            amount_flips += 1

        return result
```

Method 2 (Dynamic Programming, Time Complexity: $O(N)$, Space Complexity: $O(K)$ (K: value of `k`)) :
```python
class Solution:
    def minKBitFlips(self, nums: List[int], k: int) -> int:
        n = len(nums)
        dp = [False] * k
        amount_flips = 0
        result = 0
        for index in range(n):
            if index >= k and dp[index%k]:
                amount_flips -= 1

            if amount_flips % 2 != nums[index]:
                dp[index%k] = False
                continue

            if index+k-1 >= n:
                result = -1
                break

            result += 1
            dp[index%k] = True
            amount_flips += 1

        return result
```

Method 3 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def minKBitFlips(self, nums: List[int], k: int) -> int:
        n = len(nums)
        amount_flips = 0
        result = 0
        for index in range(n):
            if index >= k and nums[index-k] < 0:
                amount_flips -= 1

            if amount_flips % 2 != nums[index]:
                continue

            if index+k-1 >= n:
                result = -1
                break

            result += 1
            nums[index] = -1
            amount_flips += 1

        return result
```
