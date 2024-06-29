![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2285. [Maximum Total Importance Of Roads](https://leetcode.com/problems/maximum-total-importance-of-roads)

### Solution :

Method 1 (Greedy, Time Complexity: $O(M+N*Log(N))$ (M: number of elements in `roads`, N: value of `n`), Space Complexity: $O(N)$) :
```python
class Solution:
    def maximumImportance(self, n: int, roads: List[List[int]]) -> int:
        counter = [0] * n
        for a, b in roads:
            counter[a] += 1
            counter[b] += 1

        counter = sorted(enumerate(counter), key=lambda item: item[1], reverse=True)
        result = 0
        for _, amount in counter:
            result += amount * n
            n -= 1

        return result
```

Method 2 (Greedy + Counting Sort, Time Complexity: $O(M+N)$ (M: number of elements in `roads`, N: value of `n`), Space Complexity: $O(N)$) :
```python
class Solution:
    def maximumImportance(self, n: int, roads: List[List[int]]) -> int:
        counter = [0] * n
        for a, b in roads:
            counter[a] += 1
            counter[b] += 1

        counter = self.counting_sort(counter)

        result = 0
        for amount in counter[::-1]:
            result += amount * n
            n -= 1

        return result

    def counting_sort(self, nums: list[int]) -> list[int]:
        n = len(nums)
        mapping = [0] * (n+1)
        for num in nums:
            mapping[num] += 1

        prefix_sum = []
        current = 0
        for amount in mapping:
            current += amount
            prefix_sum.append(current)

        result = [0] * n
        for num in nums:
            prefix_sum[num] -= 1
            result[prefix_sum[num]] = num

        return result
```
