![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1208. [Get Equal Substrings Within Budget](https://leetcode.com/problems/get-equal-substrings-within-budget)

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def equalSubstring(self, s: str, t: str, max_cost: int) -> int:
        costs = [abs(ord(char_s)-ord(char_t)) for char_s, char_t in zip(s, t)]
        result = 0
        cost_sum = 0
        index_start = 0
        for index_end in range(len(s)):
            cost_sum += costs[index_end]
            if cost_sum <= max_cost:
                result = max(result, index_end - index_start + 1)
            else:
                while cost_sum > max_cost:
                    cost_sum -= costs[index_start]
                    index_start += 1

        return result
```
