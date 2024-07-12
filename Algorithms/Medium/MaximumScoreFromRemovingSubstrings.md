![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1717. [Maximum Score From Removing Substrings](https://leetcode.com/problems/maximum-score-from-removing-substrings)

### Solution :

Method 1 (Brute Force + Counting, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def maximumGain(self, s: str, x: int, y: int) -> int:
        amount_a, amount_b = 0, 0
        points_ab = 0
        for char in s:
            if char == 'a':
                amount_a += 1
            elif char == 'b':
                if amount_a:
                    points_ab += x
                    amount_a -= 1
                else:
                    amount_b += 1
            else:
                points_ab += min(amount_a, amount_b) * y
                amount_a, amount_b = 0, 0

        points_ab += min(amount_a, amount_b) * y

        amount_a, amount_b = 0, 0
        points_ba = 0
        for char in s:
            if char == 'b':
                amount_b += 1
            elif char == 'a':
                if amount_b:
                    points_ba += y
                    amount_b -= 1
                else:
                    amount_a += 1
            else:
                points_ba += min(amount_a, amount_b) * x
                amount_a, amount_b = 0, 0

        points_ba += min(amount_a, amount_b) * x

        return max(points_ab, points_ba)
```
