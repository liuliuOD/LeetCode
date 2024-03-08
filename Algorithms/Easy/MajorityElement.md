![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 169. [Majority Element](https://leetcode.com/problems/majority-element)

### Solution :

Method 1 (Sorting, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        nums.sort()
        return nums[len(nums) // 2]
```

Method 2 (Hash Map, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        counter = Counter(nums)
        # Option 1
        result = (0, 0)
        for num, amount in counter.items():
            if amount > result[1]:
                result = (num, amount)

        return result[0]
        """
        # Option 2

        n = len(nums)
        for num, amount in counter.items():
            if amount > n // 2:
                return num

        return None
        """
```

Method 3 (Boyer-Moore Majority Voting Algorithm, Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        result = None
        amount = 0
        for num in nums:
            if result == num:
                amount += 1
            elif amount > 0:
                amount -= 1
            else:
                result = num
                amount = 1

        return result
```
