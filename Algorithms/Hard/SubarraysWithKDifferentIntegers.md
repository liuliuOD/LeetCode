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
