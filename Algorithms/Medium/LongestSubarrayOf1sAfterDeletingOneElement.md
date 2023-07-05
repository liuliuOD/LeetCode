![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1493. [Longest Subarray Of 1's After Deleting One Element](https://leetcode.com/problems/longest-subarray-of-1s-after-deleting-one-element)

### Solution :

Method 1 (Brute Force) :
```python
class Solution:
    def longestSubarray(self, nums: List[int]) -> int:
        sublist = []
        temp = [None, None]
        for index, num in enumerate(nums):
            if num == 0:
                if temp[0] is not None:
                    sublist.append(temp)
                temp = [None, None]
                continue
            
            if temp[0] is None:
                temp[0] = index
            temp[1] = index
        
        if temp[0] is not None:
            sublist.append(temp)

        result = sublist[0][1] - sublist[0][0] if len(sublist) > 0 else 0
        if len(sublist) and result+1 < len(nums):
            result += 1
        for index_sublist in range(len(sublist)-1):
            len_sublist_1 = sublist[index_sublist][1] - sublist[index_sublist][0] + 1
            len_sublist_2 = sublist[index_sublist+1][1] - sublist[index_sublist+1][0] + 1
            len_merge = len_sublist_1 + len_sublist_2 if sublist[index_sublist+1][0] - sublist[index_sublist][1] <= 2 else len_sublist_1
            
            result = max(result, len_merge)
        
        return result
```

Method 2 (Two Pointer) :
```python
class Solution:
    def longestSubarray(self, nums: List[int]) -> int:
        result = 0
        pointer_left = 0
        pointer_right = 0
        is_all_one = True
        zeros = deque([])
        while pointer_right < len(nums):
            if nums[pointer_right] == 0:
                is_all_one = False
                zeros.append(pointer_right)
                result = max(result, pointer_right - pointer_left + 1 - len(zeros))
                if len(zeros) > 1:
                    pointer_left = zeros.popleft() + 1

            pointer_right += 1
        
        result = max(result, pointer_right - pointer_left - len(zeros))
        # based on problem description, you need to delete 1 element even if all of nums are one, so need to substract 1
        if is_all_one:
            result -= 1
        
        return result
```

Method 3 (Two Pointer, use result length to decide if all of elements in nums are one) :
```python
class Solution:
    def longestSubarray(self, nums: List[int]) -> int:
        n = len(nums)
        result = 0
        pointer_left = 0
        pointer_right = 0
        zeros = deque([])
        while pointer_right < n:
            if nums[pointer_right] == 0:
                zeros.append(pointer_right)
                result = max(result, pointer_right - pointer_left + 1 - len(zeros))
                if len(zeros) > 1:
                    pointer_left = zeros.popleft() + 1

            pointer_right += 1
        
        result = max(result, pointer_right - pointer_left - len(zeros))
        if result == n:
            result -= 1
        
        return result
```
