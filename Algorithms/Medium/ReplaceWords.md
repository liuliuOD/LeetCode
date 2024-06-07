![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 648. [Replace Words](https://leetcode.com/problems/replace-words)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(M*N*Q)$ (M: average length of the words in `sentence` and `dictionary`, N: amount of the words in `sentence`, Q: amount of the words in `dictionary`), Space Complexity: $O(M*N)$) :
```python
class Solution:
    def replaceWords(self, dictionary: List[str], sentence: str) -> str:
        result = sentence.split(" ")
        dictionary.sort()
        for index in range(len(result)):
            for root in dictionary:
                if result[index].startswith(root):
                    result[index] = root
                    break

        return " ".join(result)
```

Method 2 (Hash Set, Time Complexity: $O(M*(N+Q))$ (M: average length of the words in `sentence` and `dictionary`, N: amount of the words in `sentence`, Q: amount of the words in `dictionary`), Space Complexity: $O(M*(N+Q))$) :
```python
class Solution:
    def replaceWords(self, dictionary: List[str], sentence: str) -> str:
        result = sentence.split(" ")
        dictionary_set = set(dictionary)
        for index in range(len(result)):
            derive = result[index]
            for index_derive in range(len(derive)):
                if derive[:index_derive+1] in dictionary_set:
                    result[index] = derive[:index_derive+1]
                    break

        return " ".join(result)
```
