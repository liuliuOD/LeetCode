![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1248. [Count Number Of Nice Subarrays](https://leetcode.com/problems/count-number-of-nice-subarrays)

### Solution :

Method 1 (Mathematic + Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def numberOfSubarrays(self, nums: List[int], k: int) -> int:
        n = len(nums)
        index_odds = list(filter(lambda index: nums[index] % 2 == 1, range(n)))
        result = 0
        for index, index_odd in enumerate(index_odds):
            if index < k-1:
                continue

            left = 1
            if index == k-1:
                left += index_odds[0]
            else:
                left += index_odds[index-k+1] - index_odds[index-k] - 1

            right = 1
            if index == len(index_odds)-1:
                right += n - index_odds[-1] - 1
            else:
                right += index_odds[index+1] - index_odds[index] - 1

            result += left * right

        return result
```

Method 2 (Prefix Sum, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def numberOfSubarrays(self, nums: List[int], k: int) -> int:
        cumulative = 0
        prefix_sum = defaultdict(int)
        prefix_sum[0] = 1
        result = 0
        for num in nums:
            cumulative += num % 2
            if cumulative-k in prefix_sum:
                result += prefix_sum[cumulative - k]

            prefix_sum[cumulative] += 1

        return result
```

Method 3 (Queue, Time Complexity: $O(N)$ (N: length of `nums`), Space Complexity: $O(K)$ (K: value of `k`)) :
```python
class Solution:
    def numberOfSubarrays(self, nums: List[int], k: int) -> int:
        queue = deque()
        index_previous = -1
        result = 0
        for index, num in enumerate(nums):
            if num % 2 == 1:
                queue.append(index)

            if len(queue) > k:
                index_previous = queue.popleft()

            if len(queue) == k:
                result += queue[0] - index_previous

        return result
```
