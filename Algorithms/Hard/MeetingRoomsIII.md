![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2402. [Meeting Rooms III](https://leetcode.com/problems/meeting-rooms-iii)

### Solution :

Method 1 (Binary Heap, Time Complexity: $O(M*Log(M)+M*Log(N))$ (N: value of `n`, M: length of `meetings`), Space Complexity: $O(N+M)$) :
```python
class Solution:
    def mostBooked(self, n: int, meetings: List[List[int]]) -> int:
        heap_rooms_available = list(range(n))
        heap_rooms_using = []

        result = [0] * n
        # Option 1
        for meeting in sorted(meetings):
            start, end = meeting
        """
        # Option 2

        for start, end in sorted(meetings):
        """
            while heap_rooms_using and heap_rooms_using[0][0] <= start:
                heapq.heappush(heap_rooms_available, heapq.heappop(heap_rooms_using)[1])

            if heap_rooms_available:
                index_room = heapq.heappop(heap_rooms_available)
                heapq.heappush(heap_rooms_using, (end, index_room))
            else:
                end_previous, index_room = heapq.heappop(heap_rooms_using)
                heapq.heappush(heap_rooms_using, (end_previous + end - start, index_room))

            result[index_room] += 1

        return result.index(max(result))
```
