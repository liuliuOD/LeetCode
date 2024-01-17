![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1207. [Unique Number Of Occurrences](https://leetcode.com/problems/unique-number-of-occurrences)

### Solution :

Method 1 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def uniqueOccurrences(self, arr: List[int]) -> bool:
        frequencies = defaultdict(int)
        for item in arr:
            frequencies[item] += 1

        # Option 1
        for amount in Counter(frequencies.values()).values():
            if amount > 1:
                return False

        return True
        """
        # Option 2

        return all([amount <= 1 for amount in Counter(frequencies.values()).values()])
        """
```
