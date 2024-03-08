![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2718. [Sum Of Matrix After Queries](https://leetcode.com/problems/sum-of-matrix-after-queries)

### Solution :

Method 1 (In weekly contest 348, ERROR: "Time Limit Exceeded") :
```python
class Solution:
    def matrixSumQueries(self, n: int, queries: List[List[int]]) -> int:
        result = [0 for _ in range(n*n)]
        for q in queries:
            type_q, index, value = q
            if type_q == 0:
                for i in range(index*n, (index+1)*n):
                    result[i] = value    

            elif type_q == 1:
                for i in range(index, len(result), n):
                    result[i] = value
            
        return sum(result)
```

Method 2 :
```python
class Solution:
    def matrixSumQueries(self, n: int, queries: List[List[int]]) -> int:
        result = 0
        visited_rows = set()
        visited_columns = set()
        # Reverse the order of queries can help us to get the latest value
        for index in reversed(range(0, len(queries))):
            type_query, index_query, value_query = queries[index]
            if type_query == 0 and index_query not in visited_rows:
                visited_rows.add(index_query)
                result += value_query * (n - len(visited_columns))
            elif type_query == 1 and index_query not in visited_columns:
                visited_columns.add(index_query)
                result += value_query * (n - len(visited_rows))
        return result
```
