![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1095. [Find In Mountain Array](https://leetcode.com/problems/find-in-mountain-array)

### Constraints:

- Submissions making more than 100 calls to MountainArray.get will be judged Wrong Answer.

### Solution :

Method 1 (Binary Search) :
```python
# """
# This is MountainArray's API interface.
# You should not implement it, or speculate about its implementation
# """
#class MountainArray:
#    def get(self, index: int) -> int:
#    def length(self) -> int:

class Solution:
    def findInMountainArray(self, target: int, mountain_arr: 'MountainArray') -> int:
        n = mountain_arr.length()

        # Find index of the top of mountain
        left = 1
        right = n - 1
        while left <= right:
            middle = left + (right-left)//2
            previous = mountain_arr.get(middle-1)
            current = mountain_arr.get(middle)

            if previous > current:
                right = middle - 1
            else:
                left = middle + 1

        # Option 1
        index_top = left - 1
        """
        # Option 2

        index_top = right
        """
        # Find the `target` in the left-side of the top index
        left = 0
        right = index_top
        while left <= right:
            middle = left + (right-left)//2
            current = mountain_arr.get(middle)
            if current == target:
                return middle
            elif current < target:
                left = middle + 1
            elif current > target:
                right = middle - 1

        # Find the `target` in the right-side of the top index
        left = index_top + 1
        right = n - 1
        while left <= right:
            middle = left + (right-left)//2
            current = mountain_arr.get(middle)
            if current == target:
                return middle
            elif current < target:
                right = middle - 1
            elif current > target:
                left = middle + 1

        return -1
```
