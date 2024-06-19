![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1482. [Minimum Number Of Days To Make M Bouquets](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets)

### Solution :

Method 1 (Binary Search, Time Complexity: $O(N*Log(N))$ (N: length of `bloom_day`), Space Complexity: $O(N)$) :
```python
class Solution:
    def minDays(self, bloom_day: List[int], m: int, k: int) -> int:
        n = len(bloom_day)
        ordered_bloom_day = sorted(set(bloom_day))
        left, right = 0, len(ordered_bloom_day)-1
        while left <= right:
            middle = left + (right - left)//2
            m_temp = 0
            amount_cumulative = 0
            for index in range(n):
                if bloom_day[index] <= ordered_bloom_day[middle]:
                    amount_cumulative += 1
                else:
                    amount_cumulative = 0

                if amount_cumulative == k:
                    m_temp += 1
                    amount_cumulative = 0

            if m_temp >= m:
                right = middle - 1
            else:
                left = middle + 1

        return ordered_bloom_day[left] if left < len(ordered_bloom_day) else -1
```

Method 2 (Binary Search, Time Complexity: $O(N*Log(M))$ (M: difference between minimum of `bloom_day` and maximum of `bloom_day`, N: length of `bloom_day`), Space Complexity: $O(1)$) :
```python
class Solution:
    def minDays(self, bloom_day: List[int], m: int, k: int) -> int:
        left, right = min(bloom_day), max(bloom_day)
        while left <= right:
            middle = left + (right - left)//2
            m_temp = 0
            amount_cumulative = 0
            for day in bloom_day:
                if day <= middle:
                    amount_cumulative += 1
                    if amount_cumulative != k:
                        continue

                    m_temp += 1
                    if m_temp > m:
                        break

                amount_cumulative = 0

            if m_temp >= m:
                right = middle - 1
            else:
                left = middle + 1

        return left if left <= max(bloom_day) else -1
```
