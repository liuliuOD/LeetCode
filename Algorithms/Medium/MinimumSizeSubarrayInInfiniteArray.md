![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2875. [Minimum Size Subarray In Infinite Array](https://leetcode.com/problems/minimum-size-subarray-in-infinite-array)

### Solution :

Method 1 (In weekly contest 365, Prefix Sum + Two Pointer) :
```python
class Solution:
    def minSizeSubarray(self, nums: List[int], target: int) -> int:
        nums_target = nums.copy()
        total = sum(nums_target)
        while total < target:
            nums_target += nums
            total = sum(nums_target)
        nums_target += nums

        prefix_sum = []
        for num in nums_target:
            sum_current = prefix_sum[-1] if prefix_sum else 0
            prefix_sum.append(sum_current+num)

        result = float('inf')
        pointer_left = -1
        pointer_right = 0
        n = len(nums_target)
        while pointer_left <= pointer_right < n:
            while pointer_right < n and prefix_sum[pointer_right] < target:
                pointer_right += 1

            if prefix_sum[pointer_right] < target:
                continue

            if prefix_sum[pointer_right] == target:
                result = min(result, pointer_right - pointer_left)
                pointer_right += 1
                continue

            while True:
                if pointer_left < 0:
                    pointer_left += 1

                if pointer_left >= pointer_right or pointer_left >= n:
                    pointer_right += 1
                    break

                if (prefix_sum[pointer_right] - prefix_sum[pointer_left]) > target:
                    pointer_left += 1
                    continue
                elif (prefix_sum[pointer_right] - prefix_sum[pointer_left]) < target:
                    pointer_left -= 1
                    pointer_right += 1
                    break
                elif (prefix_sum[pointer_right] - prefix_sum[pointer_left]) == target:
                    result = min(result, pointer_right - pointer_left)
                    pointer_right += 1
                    break

        return result if result != float('inf') else -1
```

Method 2 (Hash Map) :
```python
class Solution:
    def minSizeSubarray(self, nums: List[int], target: int) -> int:
        n = len(nums)
        sum_nums = sum(nums)
        frequency = target // sum_nums
        target %= sum_nums
        if target == 0:
            return n * frequency

        result = float('inf')
        sum_current = 0
        sum_mapping = {0: -1}
        for index in range(2*n):
            sum_current += nums[index % n]
            sum_mapping[sum_current] = index

            amount_remaining = sum_current - target
            if amount_remaining in sum_mapping:
                result = min(result, index - sum_mapping[amount_remaining])

        return result + n*frequency if result != float('inf') else -1
```
