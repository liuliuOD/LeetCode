![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1347. [Minimum Number Of Steps To Make Two Strings Anagram](https://leetcode.com/problems/minimum-number-of-steps-to-make-two-strings-anagram)

### Solution :

Method 1 (HashMap, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minSteps(self, s: str, t: str) -> int:
        mapping_target = defaultdict(int)
        mapping_current = defaultdict(int)
        for char_s, char_t in zip(s, t):
            mapping_target[char_s] += 1
            mapping_current[char_t] += 1

        result = 0
        for key_target, frequency_target in mapping_target.items():
            if frequency_target < mapping_current[key_target]:
                continue

            result += frequency_target - mapping_current[key_target]

        return result
```

Method 2 :
```python
class Solution:
    def minSteps(self, s: str, t: str) -> int:
        mapping_target = defaultdict(int)
        # Option 1
        for char in s:
            mapping_target[char] += 1

        for char in t:
            mapping_target[char] -= 1
        """
        # Option 2

        for char_s, char_t in zip(s, t):
            mapping_target[char_s] += 1
            mapping_target[char_t] -= 1
        """

        result = 0
        for frequency_target in mapping_target.values():
            # Option 1
            if frequency_target < 0:
                continue

            result += frequency_target
            """
            # Option 2

            if frequency_target >= 0:
                continue

            result -= frequency_target
            """

        return result
```

Method 3 (Built-in method) :
```python
class Solution:
    def minSteps(self, s: str, t: str) -> int:
        return (Counter(s) - Counter(t)).total()
```
