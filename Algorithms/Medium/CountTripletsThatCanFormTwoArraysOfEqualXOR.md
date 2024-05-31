![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1442. [Count Triplets That Can Form Two Arrays Of Equal XOR](https://leetcode.com/problems/count-triplets-that-can-form-two-arrays-of-equal-xor)

### Solution :

Method 1 (Prefix Sum, Time Complexity: $O(N^3)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def countTriplets(self, arr: List[int]) -> int:
        n = len(arr)
        prefix_sum = [0]
        for index in range(n):
            prefix_sum.append(prefix_sum[-1] ^ arr[index])

        result = 0
        for index_k in range(n):
            for index_i in range(index_k):
                for index_j in range(index_i+1, index_k+1):
                    if prefix_sum[index_j]^prefix_sum[index_i] == prefix_sum[index_k+1]^prefix_sum[index_j]:
                        result += 1

        return result
```

Method 2 (Prefix Sum + XOR, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def countTriplets(self, arr: List[int]) -> int:
        n = len(arr)
        prefix_sum = [0]
        for index in range(n):
            prefix_sum.append(prefix_sum[-1] ^ arr[index])

        result = 0
        for index_k in range(n):
            for index_i in range(index_k):
                if prefix_sum[index_k+1] == prefix_sum[index_i]:
                    result += index_k - index_i

        return result
```
