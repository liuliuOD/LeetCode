![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1051. [Height Checker](https://leetcode.com/problems/power-of-four)

### Solution :

Method 1 (Built-In Sort, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def heightChecker(self, heights: List[int]) -> int:
        # Option 1
        heights_ordered = sorted(heights.copy())
        """
        # Option 2

        heights_ordered = sorted(heights[:])
        """
        """
        # Option 3

        heights_ordered = heights[:]
        heights_ordered.sort()
        """
        result = 0
        for index in range(len(heights)):
            if heights[index] != heights_ordered[index]:
                result += 1

        return result
```

Method 2 (Counting Sort, Time Complexity: $O(N+K)$ (N: length of `heights`, K: the difference between the minimum and the maximum in `heights`), Space Complexity: $O(N)$) :
```python
class Solution:
    def heightChecker(self, heights: List[int]) -> int:
        heights_ordered = self.counting_sort(heights[:])

        result = 0
        for index in range(len(heights)):
            if heights[index] != heights_ordered[index]:
                result += 1

        return result

    def counting_sort(self, nums: list[int]) -> list[int]:
        # Option 1
        frequency = [0] * 101
        for num in nums:
            frequency[num] += 1

        prefix_sum = [0] * 101
        for index in range(1, 101):
            prefix_sum[index] = prefix_sum[index-1] + frequency[index]

        result = [0] * len(nums)
        for num in nums:
            prefix_sum[num] -= 1
            result[prefix_sum[num]] = num

        return result
        """
        # Option 2

        frequency = [0] * 101
        minimum, maximum = inf, -inf
        for num in nums:
            frequency[num] += 1
            minimum = min(minimum, num)
            maximum = max(maximum, num)

        result = []
        for num in range(minimum, maximum+1):
            while frequency[num]:
                frequency[num] -= 1
                result.append(num)

        return result
        """
        """
        # Option 3

        frequency = [0] * 101
        minimum, maximum = inf, -inf
        for num in nums:
            frequency[num] += 1
            minimum = min(minimum, num)
            maximum = max(maximum, num)

        result = []
        while minimum <= maximum:
            if frequency[minimum]:
                result.append(minimum)

            frequency[minimum] -= 1
            if frequency[minimum] <= 0:
                minimum += 1

        return result
        """
```

Method 3 (Radix Sort, Time Complexity: $O(N*D)$ (N: length of `heights`, D: the number of digits of the maximum element in `heights`), Space Complexity: $O(N)$) :
```python
BASE = 10

class Solution:
    def heightChecker(self, heights: List[int]) -> int:
        heights_sorted = heights[:]
        self.radix_sort(heights_sorted)

        result = 0
        for index in range(len(heights)):
            if heights[index] != heights_sorted[index]:
                result += 1

        return result

    def radix_sort(self, nums: list[int]) -> None:
        maximum = max(nums)
        maximum_digits = len(str(maximum))
        for digit in range(maximum_digits):
            self.bucket_sort(nums, BASE**digit)

    def bucket_sort(self, nums: list[int], divider: int) -> None:
        buckets = [[] for _ in range(BASE)]
        for num in nums:
            buckets[(num // divider)%BASE].append(num)

        index_num = 0
        for index in range(BASE):
            for num in buckets[index]:
                nums[index_num] = num
                index_num += 1
```
