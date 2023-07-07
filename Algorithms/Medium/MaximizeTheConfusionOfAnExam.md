![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2024. [Maximize The Confusion Of An Exam](https://leetcode.com/problems/maximize-the-confusion-of-an-exam)

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N)$) :
```python
class Solution:
    def maxConsecutiveAnswers(self, answerKey: str, k: int) -> int:
        n = len(answerKey)

        result = 0
        amount_T = 0
        amount_F = 0
        pointer_left = 0
        pointer_right = 0
        while pointer_left <= pointer_right and pointer_right < n:
            if answerKey[pointer_right] == 'T':
                amount_T += 1
            elif answerKey[pointer_right] == 'F':
                amount_F += 1
            
            while min(amount_T, amount_F) > k:
                if answerKey[pointer_left] == 'T':
                    amount_T -= 1
                elif answerKey[pointer_left] == 'F':
                    amount_F -= 1
                pointer_left += 1

            result = max(result, amount_T + amount_F)
            pointer_right += 1
        
        return result
```

Method 2 (Two Pointer, Time Complexity: $O(N)$) :
```python
class Solution:
    def maxConsecutiveAnswers(self, answerKey: str, k: int) -> int:
        n = len(answerKey)
        self.answerKey = answerKey

        amount_T, amount_F = 0, 0
        pointer_left, pointer_right = 0, 0
        result = 0
        while pointer_left <= pointer_right and pointer_right < n:
            if self.isTrue(pointer_right):
                amount_T += 1
            elif self.isFalse(pointer_right):
                amount_F += 1
            
            while min(amount_T, amount_F) > k:
                if self.isTrue(pointer_left):
                    amount_T -= 1
                elif self.isFalse(pointer_left):
                    amount_F -= 1
                pointer_left += 1

            result = max(result, amount_T + amount_F)
            pointer_right += 1
        
        return result

    def isTrue(self, index: int) -> bool:
        return self.answerKey[index] == 'T'
    
    def isFalse(self, index: int) -> bool:
        return self.answerKey[index] == 'F'
```

Method 3 (Two Pointer, Time Complexity: $O(2*N)$ => $O(N)$) :
```python
class Solution:
    def maxConsecutiveAnswers(self, answerKey: str, k: int) -> int:
        self.k = k
        self.n = len(answerKey)
        self.answerKey = answerKey

        return max(self.findConsecutiveChar('T'), self.findConsecutiveChar('F'))

    def findConsecutiveChar(self, ch: str) -> int:
        amount_non_ch = 0
        pointer_left = -1
        length_consecutive = 0
        for index in range(self.n):
            if self.answerKey[index] != ch:
                amount_non_ch += 1
                if amount_non_ch > self.k:
                    pointer_left += 1
                    while pointer_left < self.n and self.answerKey[pointer_left] == ch:
                        pointer_left += 1

            length_consecutive = max(length_consecutive, index - pointer_left)

        return length_consecutive
```
