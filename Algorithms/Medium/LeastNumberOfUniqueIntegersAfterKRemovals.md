![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1481. [Least Number Of Unique Integers After K Removals](https://leetcode.com/problems/least-number-of-unique-integers-after-k-removals)

### Solution :

Method 1 (Binary Heap, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findLeastNumOfUniqueInts(self, arr: List[int], k: int) -> int:
        counter = Counter(arr)
        heap = []
        for amount in counter.values():
            heapq.heappush(heap, amount)

        while heap and k:
            current = heapq.heappop(heap)
            if current > k:
                heapq.heappush(heap, current-k)
                break

            k -= current

        return len(heap)
```

Method 2 (Sorting, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findLeastNumOfUniqueInts(self, arr: List[int], k: int) -> int:
        counter = Counter(arr)
        order = sorted(counter.values(), reverse=True)
        while order and k:
            current = order.pop()
            if current > k:
                order.append(current-k)
                break

            k -= current

        return len(order)
```
