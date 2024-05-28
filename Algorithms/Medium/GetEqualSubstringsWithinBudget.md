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

Method 2 (Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def equalSubstring(self, s: str, t: str, max_cost: int) -> int:
        result = 0
        cost_sum = 0
        index_start = 0
        for index_end in range(len(s)):
            cost_sum += abs(ord(s[index_end])-ord(t[index_end]))
            if cost_sum <= max_cost:
                result = max(result, index_end - index_start + 1)
            else:
                while cost_sum > max_cost:
                    cost_sum -= abs(ord(s[index_start])-ord(t[index_start]))
                    index_start += 1

        return result
```

Method 3 (Two Pointer + Refactoring, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def equalSubstring(self, s: str, t: str, max_cost: int) -> int:
        result = 0
        cost_sum = 0
        index_start = 0
        for index_end in range(len(s)):
            cost_sum += self.get_cost(index_end, s, t)
            if cost_sum <= max_cost:
                result = max(result, index_end - index_start + 1)
            else:
                while cost_sum > max_cost:
                    cost_sum -= self.get_cost(index_start, s, t)
                    index_start += 1

        return result

    def get_cost(self, index: int, s: str, t: str) -> int:
        return abs(ord(s[index])-ord(t[index]))
```
