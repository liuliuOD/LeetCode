![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2765. [Longest Alternating Subarray](https://leetcode.com/problems/longest-alternating-subarray)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N^2)$) :
```python
class Solution:
    def alternatingSubarray(self, nums: List[int]) -> int:
        result = 0
        n = len(nums)
        for index in range(n):
            temp = 1
            for index_next in range(index+1, n):
                if nums[index_next]-nums[index_next-1] != (-1)**(index_next-index-1):
                    break
                temp += 1
            result = max(result, temp)
        
        return result if result > 1 else -1
```

Method 2 (Two Pointer, Time Complexity: $O(N)$) :
```python
class Solution:
    def alternatingSubarray(self, nums: List[int]) -> int:
        n = len(nums)
        pointer_left = 0
        pointer_right = pointer_left + 1

        result = -1
        while pointer_left < n:
            while pointer_right < n and nums[pointer_right] == (nums[pointer_left] + (pointer_right - pointer_left) % 2):
                result = max(result, pointer_right - pointer_left + 1)
                pointer_right += 1
            
            pointer_left = max(pointer_left+1, pointer_right-1)
            pointer_right = pointer_left + 1

        return result
```
