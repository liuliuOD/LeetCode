![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 451. [Sort Characters By Frequency](https://leetcode.com/problems/sort-characters-by-frequency)

### Solution :

Method 1 (List Comprehension, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def frequencySort(self, s: str) -> str:
        counter = Counter(s)
        return ''.join([char * amount for char, amount in sorted(counter.items(), key=lambda item: item[1], reverse=True)])
```

Method 2 (Binary Heap, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def frequencySort(self, s: str) -> str:
        counter = Counter(s)
        min_heap = [(-value, key) for key, value in counter.items()]
        heapq.heapify(min_heap)
        result = ''
        while min_heap:
            amount, char = heapq.heappop(min_heap)
            result += char * (-amount)

        return result
```
