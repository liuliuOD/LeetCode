![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1002. [Find Common Characters](https://leetcode.com/problems/find-common-characters)

### Solution :

Method 1 (Time Complexity: $O(M*N)$ (M: average length of elements in `words`, N: length of `words`), Space Complexity: $O(N)$) :
```python
class Solution:
    def commonChars(self, words: List[str]) -> List[str]:
        n = len(words)
        frequency = [Counter(word) for word in words]
        result = []
        for char in frequency[0].keys():
            amount_minimum = inf
            for index in range(n):
                if char not in frequency[index]:
                    break

                amount_minimum = min(amount_minimum, frequency[index][char])
            else:
                result.extend([char] * amount_minimum)

        return result
```

Method 2 (Time Complexity: $O(M*N)$ (M: average length of elements in `words`, N: length of `words`), Space Complexity: $O(1)$) :
```python
BASE = ord("a")
class Solution:
    def commonChars(self, words: List[str]) -> List[str]:
        n = len(words)
        frequency = [inf] * 26
        for word in words:
            counter = Counter(word)
            for offset in range(26):
                char = chr(BASE + offset)
                frequency[offset] = min(frequency[offset], counter.get(char, 0))

        result = []
        for offset, amount in enumerate(frequency):
            result += [chr(BASE+offset)] * amount
        return result
```
