![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 992. [Subarrays With K Different Integers](https://leetcode.com/problems/subarrays-with-k-different-integers)

### Solution :

Method 1 (Two Pointers, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def subarraysWithKDistinct(self, nums: List[int], k: int) -> int:
        left = 0
        counter = defaultdict(int)
        result = 0
        for right, num in enumerate(nums):
            counter[num] += 1
            result += self.shrink(left, right, nums, counter.copy(), k)

            while len(counter) > k:
                counter[nums[left]] -= 1
                if counter[nums[left]] == 0:
                    del counter[nums[left]]

                left += 1

        return result

    def shrink(self, left: int, right: int, nums: List[int], counter: Dict[int, int], k: int) -> int:
        result = 0
        while len(counter) >= k:
            if len(counter) == k:
                result += 1

            counter[nums[left]] -= 1
            if counter[nums[left]] == 0:
                del counter[nums[left]]

            left += 1

        return result
```

Method 2 (Two Pointers, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def subarraysWithKDistinct(self, nums: List[int], k: int) -> int:
        left = 0
        counter = defaultdict(int)
        result = 0
        for right, num in enumerate(nums):
            counter[num] += 1
            flag = True
            temp_left = left
            temp_counter = counter.copy()
            while len(temp_counter) >= k:
                if len(temp_counter) == k:
                    result += 1
                    if flag:
                        left = temp_left
                        counter = temp_counter.copy()
                        flag = not flag

                temp_counter[nums[temp_left]] -= 1
                if temp_counter[nums[temp_left]] == 0:
                    del temp_counter[nums[temp_left]]

                temp_left += 1

        return result
```

Method 3 (Two Pointers, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def subarraysWithKDistinct(self, nums: List[int], k: int) -> int:
        return self.atMost(k, nums) - self.atMost(k-1, nums)

    def atMost(self, k: int, nums: List[int]) -> int:
        counter = defaultdict(int)
        result = 0
        left = 0
        for right, num in enumerate(nums):
            counter[num] += 1
            while len(counter) > k:
                remove = nums[left]
                counter[remove] -= 1
                if counter[remove] == 0:
                    del counter[remove]

                left += 1

            result += right - left + 1

        return result
```
