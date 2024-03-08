![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1346. [Check If N and Its Double Exist](https://leetcode.com/problems/check-if-n-and-its-double-exist)

### Solution :

Method 1 (Binary Search) :
```python
class Solution:
    def checkIfExist(self, arr: List[int]) -> bool:
        arr.sort()
        for i in range(len(arr)):
            left = 0
            right = len(arr) - 1
            while left <= right:
                middle = left + (right - left) // 2
                if middle != i and arr[i] == arr[middle]*2:
                    return True
                
                if arr[i] > arr[middle]*2:
                    left = middle + 1
                else:
                    right = middle - 1
        return False
```
