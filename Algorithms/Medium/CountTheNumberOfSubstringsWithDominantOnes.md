![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 3234. [Count The Number Of Substrings With Dominant Ones](https://leetcode.com/problems/count-the-number-of-substrings-with-dominant-ones)

### Solution :

Method 1 (Sliding Window, Time Complexity: $O(N*\sqrt{N})$, Space Complexity: $O(N)$) :
```python
class Solution:
    def numberOfSubstrings(self, s: str) -> int:
        n = len(s)
        result = 0
        for window in range(1, int(n**0.5)+1):
            index_zero_previous = -1
            zeros = deque()
            amount_ones = 0
            for index in range(n):
                if s[index] == '0':
                    zeros.append(index)
                    if len(zeros) > window:
                        amount_ones -= zeros[0] - index_zero_previous - 1
                        index_zero_previous = zeros.popleft()
                else:
                    amount_ones += 1

                if len(zeros) == window and amount_ones >= window**2:
                    result += min(zeros[0]-index_zero_previous, amount_ones-window**2+1)

        index = 0
        while index < n:
            if s[index] == '0':
                index += 1
                continue

            amount_ones = 0
            while index < n and s[index] == '1':
                amount_ones += 1
                index += 1
                result += amount_ones

        return result
```
