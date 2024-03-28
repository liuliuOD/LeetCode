![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2958. [Length Of Longest Subarray With At Most K Frequency](https://leetcode.com/problems/length-of-longest-subarray-with-at-most-k-frequency)

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def maxSubarrayLength(self, nums: List[int], k: int) -> int:
        counter = defaultdict(int)
        left = 0
        result = 0
        for right, num in enumerate(nums):
            counter[num] += 1
            while left <= right and counter[num] > k:
                counter[nums[left]] -= 1
                left += 1

            result = max(result, right - left + 1)

        return result
```
