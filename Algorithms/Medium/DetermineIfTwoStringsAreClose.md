![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1657. [Determine If Two Strings Are Close](https://leetcode.com/problems/determine-if-two-strings-are-close)

### Solution :

Method 1 (HashMap + Set) :
```python
class Solution:
    def closeStrings(self, word_1: str, word_2: str) -> bool:
        if len(word_1) != len(word_2):
            return False

        alpha_1 = set(word_1)
        alpha_2 = set(word_2)
        if len(alpha_1 - alpha_2) or len(alpha_2 - alpha_1):
            return False

        counter_1 = Counter(word_1)
        counter_2 = Counter(word_2)
        mapping_1 = defaultdict(int)
        for char, frequency in counter_1.items():
            mapping_1[frequency] += 1
        mapping_2 = defaultdict(int)
        for char, frequency in counter_2.items():
            mapping_2[frequency] += 1

        for frequency, amount in mapping_1.items():
            if mapping_2[frequency] != amount:
                return False

        return True
```

Method 2 (List) :
```python
BASE = ord('a')
class Solution:
    def closeStrings(self, word_1: str, word_2: str) -> bool:
        frequency_1 = [0] * 26
        frequency_2 = [0] * 26
        for char in word_1:
            frequency_1[ord(char)-BASE] += 1
        for char in word_2:
            frequency_2[ord(char)-BASE] += 1

        for index in range(26):
            if (frequency_1[index] == 0 and frequency_2[index] > 0) or (frequency_1[index] > 0 and frequency_2[index] == 0):
                return False

        frequency_1.sort()
        frequency_2.sort()
        for index in range(26):
            if frequency_1[index] != frequency_2[index]:
                return False

        return True
```
