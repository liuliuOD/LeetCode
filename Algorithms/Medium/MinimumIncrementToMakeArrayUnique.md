![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 945. [Minimum Increment To Make Array Unique](https://leetcode.com/problems/minimum-increment-to-make-array-unique)

### Solution :

Method 1 (Built-In Sort, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minIncrementForUnique(self, nums: List[int]) -> int:
        counter = defaultdict(int)
        nums_ordered = set()
        for num in nums:
            counter[num] += 1
            nums_ordered.add(num)

        nums_ordered = sorted(list(nums_ordered), reverse=True)
        result = 0
        while nums_ordered:
            num = nums_ordered.pop()
            if counter[num] > 1:
                amount_remaining = counter[num] - 1
                result += amount_remaining
                counter[num+1] += amount_remaining
                if not nums_ordered or nums_ordered[-1] != num+1:
                    nums_ordered.append(num+1)

        return result
```

Method 2 (Radix Sort, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minIncrementForUnique(self, nums: List[int]) -> int:
        counter = defaultdict(int)
        nums_ordered = set()
        for num in nums:
            counter[num] += 1
            nums_ordered.add(num)

        nums_ordered = self.radix_sort(list(nums_ordered))[::-1]
        result = 0
        while nums_ordered:
            num = nums_ordered.pop()
            if counter[num] > 1:
                amount_remaining = counter[num] - 1
                result += amount_remaining
                counter[num+1] += amount_remaining
                if not nums_ordered or nums_ordered[-1] != num+1:
                    nums_ordered.append(num+1)

        return result

    def radix_sort(self, nums: list[int]) -> list[int]:
        for bit in range(6):
            nums = self.bucket_sort(nums, bit)

        return nums

    def bucket_sort(self, nums: list[int], bit: int) -> list[int]:
        buckets = [[] for _ in range(10)]
        for num in nums:
            buckets[num // (10**bit) % 10].append(num)

        index = 0
        for bucket in buckets:
            for num in bucket:
                nums[index] = num
                index += 1

        return nums
```
