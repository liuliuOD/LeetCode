![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 152. [Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray)

### Solution :

Method 1 (Brute Force, ERROR: "Time Limit Exceeded", 186/190) :
```python
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        n = len(nums)
        result = -inf
        for index in range(n):
            # Option 1
            product = nums[index]
            result = max(result, product)
            for index_end in range(index+1, n):
            """
            # Option 2

            product = 1
            for index_end in range(index, n):
            """

                product *= nums[index_end]
                result = max(result, product)

                if product == 0:
                    product = 1

        return result
```

Method 2 (Prefix Sum + Suffix Sum):
```python
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        n = len(nums)
        prefix = [[] for _ in range(n)]
        prefix[0] = [nums[0], nums[0]]
        for index in range(1, n):
            if nums[index] == 0:
                prefix[index] = [0, 0]
            elif prefix[index-1][0] == 0:
                prefix[index] = [nums[index], nums[index]]
            else:
                # record the maximum and minimum values within all contiguous sequences containing `nums[index]` from left to right
                prefix[index] = [max(prefix[index-1][0]*nums[index], prefix[index-1][1]*nums[index], nums[index]), min(prefix[index-1][0]*nums[index], prefix[index-1][1]*nums[index], nums[index])]

        suffix = [[] for _ in range(n)]
        suffix[-1] = [nums[-1], nums[-1]]
        for index in reversed(range(n-1)):
            if nums[index] == 0:
                suffix[index] = [0, 0]
            elif suffix[index+1][0] == 0:
                suffix[index] = [nums[index], nums[index]]
            else:
                # record the maximum and minimum values within all contiguous sequences containing `nums[index]` from right to left
                suffix[index] = [max(suffix[index+1][0]*nums[index], suffix[index+1][1]*nums[index], nums[index]), min(suffix[index+1][0]*nums[index], suffix[index+1][1]*nums[index], nums[index])]

        result = -inf
        for index in range(n):
            if nums[index] == 0:
                result = max(result, 0)
                continue

            result = max(result, prefix[index][0]*suffix[index][0]/nums[index], prefix[index][0]*suffix[index][1]/nums[index], prefix[index][1]*suffix[index][0]/nums[index], prefix[index][1]*suffix[index][1]/nums[index])

        return int(result)
```

Method 3 (Kadane's) :
```python
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        result = -inf
        # from left to right
        product = 1
        for num in nums:
            product *= num
            result = max(result, product)

            if product == 0:
                product = 1

        # from right to left
        product = 1
        for num in reversed(nums):
            product *= num
            result = max(result, product)

            if product == 0:
                product = 1

        return result
```

Method 4 (Kadane's) :
```python
class Solution:
    def maxProduct(self, nums: List[int]) -> int:
        n = len(nums)
        result = maximum = minimum = nums[0]
        for index in range(1, n):
            # Option 1
            maximum, minimum = max(nums[index], maximum*nums[index], minimum*nums[index]), min(nums[index], maximum*nums[index], minimum*nums[index])
            """
            # Option 2

            candidates = [nums[index], maximum*nums[index], minimum*nums[index]]
            maximum = max(candidates)
            minimum = min(candidates)
            """
            result = max(result, maximum)

        return result
```
