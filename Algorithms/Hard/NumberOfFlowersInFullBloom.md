![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2251. [Number Of Flowers In Full Bloom](https://leetcode.com/problems/number-of-flowers-in-full-bloom)

### Solution :

Method 1 (Hash Map, ERROR: "Memory Limit Exceeded") :
```python
class Solution:
    def fullBloomFlowers(self, flowers: List[List[int]], people: List[int]) -> List[int]:
        mapping = defaultdict(int)
        for start, end in flowers:
            for index in range(start, end+1):
                mapping[index] += 1

        result = []
        for person in people:
            result.append(mapping[person])

        return result
```

Method 2 (Hash Map, ERROR: "Time Limit Exceeded") :
```python
class Solution:
    def fullBloomFlowers(self, flowers: List[List[int]], people: List[int]) -> List[int]:
        mapping = {}
        for person in people:
            mapping[person] = 0

        for start, end in flowers:
            for index in range(start, end+1):
                if index not in mapping:
                    continue

                mapping[index] += 1

        result = []
        for person in people:
            result.append(mapping[person])

        return result
```

Method 3 (Binary Search, Time Complexity: $O(M*Log(N)+M*Log(M)+N*Log(N))$ (M: amount of people, N: amount of flowers)) :
```python
class Solution:
    def fullBloomFlowers(self, flowers: List[List[int]], people: List[int]) -> List[int]:
        n = len(flowers)
        started = sorted(start for start, _ in flowers)
        ended = sorted(end for _, end in flowers)
        result = []
        for person in people:
            # Find the amount of flowers that have started bloom when person visited
            left_started = 0
            right_started = n - 1
            while left_started <= right_started:
                index = left_started + (right_started - left_started) // 2
                flower = started[index]
                if flower <= person:
                    left_started = index + 1
                else:
                    right_started = index - 1

            # Find the amount of flowers that have been withered before person visited
            left_ended = 0
            right_ended = n - 1
            while left_ended <= right_ended:
                index = left_ended + (right_ended - left_ended) // 2
                flower = ended[index]
                if flower < person:
                    left_ended = index + 1
                else:
                    right_ended = index - 1

            result.append(left_started - left_ended)

        return result
```

Method 4 (Binary Heap, Time Complexity: $O(M*Log(M)+N*Log(N)+M*Log(N))$ (M: amount of people, N: amount of flowers)) :
```python
class Solution:
    def fullBloomFlowers(self, flowers: List[List[int]], people: List[int]) -> List[int]:
        people_sorted = sorted((person, index) for index, person in enumerate(people))
        flowers.sort(key=lambda item: item[0])

        result = [0] * len(people)
        index_flower = 0
        heap = []
        for person, index_person in people_sorted:
            while index_flower < len(flowers) and flowers[index_flower][0] <= person:
                heappush(heap, flowers[index_flower][1])
                index_flower += 1

            while heap and heap[0] < person:
                heappop(heap)

            result[index_person] = len(heap)

        return result
```

Method 5 (Sweep Line Algorithm + Prefix Sum) :
```python
class Solution:
    def fullBloomFlowers(self, flowers: List[List[int]], people: List[int]) -> List[int]:
        mapping = defaultdict(int)
        for start, end in flowers:
            mapping[start] += 1
            mapping[end+1] -= 1

        accumulation = 0
        prefix_sum = {}
        for key, amount in sorted(mapping.items()):
            accumulation += amount
            prefix_sum[key] = accumulation

        keys = list(prefix_sum.keys())
        result = []
        for person in people:
            left = 0
            right = len(keys) - 1
            while left <= right:
                index = left + (right-left)//2
                if keys[index] <= person:
                    left = index + 1
                else:
                    right = index - 1

            result.append(prefix_sum[keys[right]])

        return result
```
