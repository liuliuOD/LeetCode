![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2968. [Apply Operations To Maximize Frequency Score](https://leetcode.com/problems/apply-operations-to-maximize-frequency-score)

### Solution :

Method 1 (ERROR: "Time Limit Exceeded", 717/774) :
```python
class Solution:
    def maxFrequencyScore(self, nums: List[int], k: int) -> int:
        n = len(nums)
        nums.sort()
        window = n
        while window > 0:
            for left in range(0, n-window+1):
                median = nums[left+window//2] if window % 2 else round((nums[left+window//2]+nums[left-1+window//2])/2)
                cost = sum([abs(value-median) for value in nums[left:left+window]])
                if cost <= k:
                    return window

            window -= 1

        return 1
```
