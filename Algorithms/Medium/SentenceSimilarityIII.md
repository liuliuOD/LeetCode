![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1813. [Sentence Similarity III](https://leetcode.com/problems/sentence-similarity-iii)

### Solution :

Method 1 (Brute Force) :
```python
class Solution:
    def areSentencesSimilar(self, sentence1: str, sentence2: str) -> bool:
        m, n = len(sentence1), len(sentence2)
        if m > n:
            m, n = n, m
            sentence1, sentence2 = sentence2, sentence1

        if sentence1 == sentence2 or (sentence2.startswith(sentence1) and sentence2[m] == " ") or (sentence2.endswith(sentence1) and sentence2[-m-1] == " "):
            return True

        for index_left in range(m):
            if sentence1[index_left] != " ":
                continue

            if sentence2.startswith(sentence1[:index_left+1]) and sentence2.endswith(sentence1[index_left+1:]) and sentence2[index_left] == " " and sentence2[-(m-index_left)] == " ":
                return True

        return False
```
