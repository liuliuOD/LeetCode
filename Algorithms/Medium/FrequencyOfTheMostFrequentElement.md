![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1838. [Frequency Of The Most Frequent Element](https://leetcode.com/problems/frequency-of-the-most-frequent-element)

### Solution :

Method 1 (Two Pointers, Time Complexity: $O(N*Log(N))$, Space Complexity: $O()$ (doesn't use any extra space, so the `SC` depends on the implementation of each programming language)) :
```python
class Solution:
    def maxFrequency(self, nums: List[int], k: int) -> int:
        nums.sort()

        result = 1
        n = len(nums)
        sum_of_window = 0
        # Option 1
        left = right = 0
        while right < n:
            sum_of_window += nums[right]
            while right > left and nums[right] * (right-left+1) - sum_of_window > k:
                sum_of_window -= nums[left]
                left += 1

            result = max(result, right-left+1)
            right += 1
        """
        # Option 2

        left = 0
        for right in range(n):
            sum_of_window += nums[right]
            while right > left and nums[right] * (right-left+1) - sum_of_window > k:
                sum_of_window -= nums[left]
                left += 1

            result = max(result, right-left+1)
        """

        return result
```

Method 2 :
```python
class Solution:
    def maxFrequency(self, nums: List[int], k: int) -> int:
        nums.sort()

        left = 0
        n = len(nums)
        sum_of_window = 0
        # Option 1
        result = 1
        for right in range(n):
            sum_of_window += nums[right]
            if nums[right] * (right-left+1) - sum_of_window > k:
                sum_of_window -= nums[left]
                left += 1

            result = max(result, right-left+1)

        return result
        """
        # Option 2

        for right in range(n):
            sum_of_window += nums[right]
            if nums[right] * (right-left+1) - sum_of_window > k:
                sum_of_window -= nums[left]
                left += 1

        return n - left
        """
```
