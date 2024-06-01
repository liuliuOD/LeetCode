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

Method 3 ([Prefix Sum + Hash Map](https://leetcode.com/problems/count-triplets-that-can-form-two-arrays-of-equal-xor/editorial), Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def countTriplets(self, arr: List[int]) -> int:
        n = len(arr)
        prefix_xor = [0]
        for index in range(n):
            prefix_xor.append(prefix_xor[-1] ^ arr[index])

        xor_frequency, xor_amount_triplet = defaultdict(int), defaultdict(int)
        result = 0
        for index, xor_prefix in enumerate(prefix_xor):
            result += xor_frequency[xor_prefix]*(index - 1) - xor_amount_triplet[xor_prefix]

            xor_frequency[xor_prefix] += 1
            xor_amount_triplet[xor_prefix] += index

        return result
```

Method 4 ([Prefix Sum + Hash Map](https://leetcode.com/problems/count-triplets-that-can-form-two-arrays-of-equal-xor/editorial), Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def countTriplets(self, arr: List[int]) -> int:
        n = len(arr)
        xor_frequency, xor_amount_triplet = defaultdict(int), defaultdict(int)
        xor_frequency[0] = 1
        prefix_xor = [0]
        result = 0
        for index in range(n):
            prefix_xor.append(prefix_xor[-1] ^ arr[index])
            prefix_xor_current = prefix_xor[-1]
            result += xor_frequency[prefix_xor_current]*index - xor_amount_triplet[prefix_xor_current]

            xor_frequency[prefix_xor_current] += 1
            xor_amount_triplet[prefix_xor_current] += index + 1

        return result
```
