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
            # Option 1
            current = order.pop()
            if current > k:
                order.append(current-k)
                break

            k -= current
            """
            # Option 2

            if order[-1] > k:
                break

            k -= order.pop()
            """

        return len(order)
```

Method 3 (Counting Sort, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findLeastNumOfUniqueInts(self, arr: List[int], k: int) -> int:
        n = len(arr)
        counter = Counter(arr).values()
        prefix_sum = [0] * (n+1)
        for amount in counter:
            prefix_sum[amount] += 1

        for index in range(1, len(prefix_sum)):
            prefix_sum[index] = prefix_sum[index-1] + prefix_sum[index]

        ordered = [0] * len(counter)
        for target in reversed(counter):
            prefix_sum[target] -= 1
            ordered[prefix_sum[target]] = target

        ordered = list(reversed(ordered))
        while k:
            if ordered[-1] > k:
                break

            k -= ordered.pop()

        return len(ordered)
```

Method 4 (Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findLeastNumOfUniqueInts(self, arr: List[int], k: int) -> int:
        n = len(arr)
        counter = Counter(arr).values()
        frequencies = [0] * (n+1)
        for amount in counter:
            frequencies[amount] += 1

        result = len(counter)
        for amount in range(1, n+1):
            if k < amount:
                break

            amount_remove = min(k // amount, frequencies[amount])
            k -= amount_remove * amount
            result -= amount_remove

        return result
```
