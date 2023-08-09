![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2616. [Minimize The Maximum Difference Of Pairs](https://leetcode.com/problems/minimize-the-maximum-difference-of-pairs)

### Solution :

Method 1 (Binary Search + Greedy) :
```python
class Solution:
    def minimizeMax(self, nums: List[int], p: int) -> int:
        nums.sort()
        low = 0
        high = nums[-1] - nums[0]

        while low <= high:
            middle = low + (high-low)//2

            if self.canPair(middle, nums, p):
                high = middle - 1
            else:
                low = middle + 1

        return low

    def canPair(self, difference: int, nums: List[int], p: int) -> bool:
        pair_amount = 0
        index = 1
        while index < len(nums) and pair_amount < p:
            if nums[index] - nums[index-1] <= difference:
                pair_amount += 1
                index += 2
                continue

            index += 1

        return pair_amount == p
```
