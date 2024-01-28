![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1074. [Number Of Submatrices That Sum To Target](https://leetcode.com/problems/number-of-submatrices-that-sum-to-target)

### Solution :

Method 1 (Prefix Sum, ERROR: "Time Limit Exceeded", 40/40) :
```python
class Solution:
    def numSubmatrixSumTarget(self, matrix: List[List[int]], target: int) -> int:
        m = len(matrix)
        n = len(matrix[0])
        prefix_sum = [[0]*(n+1) for _ in range(m+1)]
        for index_m in range(1, m+1):
            for index_n in range(1, n+1):
                prefix_sum[index_m][index_n] = prefix_sum[index_m][index_n-1] + prefix_sum[index_m-1][index_n] - prefix_sum[index_m-1][index_n-1] + matrix[index_m-1][index_n-1]

        result = 0
        for index_m_end in range(1, m+1):
            for index_n_end in range(1, n+1):
                for index_m_start in range(1, index_m_end+1):
                    for index_n_start in range(1, index_n_end+1):
                        temp = prefix_sum[index_m_end][index_n_end] - prefix_sum[index_m_end][index_n_start-1] - prefix_sum[index_m_start-1][index_n_end] + prefix_sum[index_m_start-1][index_n_start-1]
                        if temp == target:
                            result += 1

        return result
```

Method 2 (Prefix Sum, Time Complexity: $O(M*N^2)$, Space Complexity: $O(M*N)$) :
```python
class Solution:
    def numSubmatrixSumTarget(self, matrix: List[List[int]], target: int) -> int:
        m = len(matrix)
        n = len(matrix[0])
        prefix_sum = [[0]*(n+1) for _ in range(m+1)]
        for index_m in range(1, m+1):
            for index_n in range(1, n+1):
                prefix_sum[index_m][index_n] = prefix_sum[index_m][index_n-1] + matrix[index_m-1][index_n-1]

        result = 0
        for index_n_start in range(1, n+1):
            for index_n_end in range(index_n_start, n+1):
                mapping = defaultdict(int)
                mapping[0] = 1
                summarize = 0
                for index_m in range(1, m+1):
                    summarize += prefix_sum[index_m][index_n_end] - (0 if index_n_start <= 1 else prefix_sum[index_m][index_n_start-1])
                    result += mapping[summarize-target]
                    mapping[summarize] += 1

        return result
```

Method 3 (Prefix Sum, Time Complexity: $O(M*N^2)$, Space Complexity: $O(M)$) :
```python
class Solution:
    def numSubmatrixSumTarget(self, matrix: List[List[int]], target: int) -> int:
        m = len(matrix)
        n = len(matrix[0])
        for index_m in range(m):
            for index_n in range(1, n):
                matrix[index_m][index_n] += matrix[index_m][index_n-1]

        result = 0
        for index_n_start in range(n):
            for index_n_end in range(index_n_start, n):
                mapping = defaultdict(int)
                mapping[0] = 1
                summarize = 0
                for index_m in range(m):
                    summarize += matrix[index_m][index_n_end] - (0 if index_n_start <= 0 else matrix[index_m][index_n_start-1])
                    result += mapping[summarize-target]
                    mapping[summarize] += 1

        return result
```
