![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2391. [Minimum Amount Of Time To Collect Garbage](https://leetcode.com/problems/minimum-amount-of-time-to-collect-garbage)

### Solution :

Method 1 (Time Complexity: $O(M*N)$ (M: amount of `garbage`, N: maximum length of the item in `garbage`), Space Complexity: $O(N)$) :
```python
class Solution:
    def garbageCollection(self, garbage: List[str], travel: List[int]) -> int:
        n = len(garbage)
        index_maximum = {}
        mapping = [defaultdict(int) for _ in range(n)]
        for index in range(n):
            for char in garbage[index]:
                mapping[index][char] += 1
                index_maximum[char] = index

        result = 0
        # M
        char = 'M'
        for index in range(n):
            if char not in index_maximum or index_maximum[char] < index:
                break

            if index > 0:
                result += travel[index-1]

            if char in mapping[index]:
                result += mapping[index][char]

        # P
        char = 'P'
        for index in range(n):
            if char not in index_maximum or index_maximum[char] < index:
                break

            if index > 0:
                result += travel[index-1]

            if char in mapping[index]:
                result += mapping[index][char]

        # G
        char = 'G'
        for index in range(n):
            if char not in index_maximum or index_maximum[char] < index:
                break

            if index > 0:
                result += travel[index-1]

            if char in mapping[index]:
                result += mapping[index][char]

        return result
```

Method 2 (Clean Code) :
```python
class Solution:
    def garbageCollection(self, garbage: List[str], travel: List[int]) -> int:
        n = len(garbage)
        index_maximum = {}
        mapping = [defaultdict(int) for _ in range(n)]
        for index in range(n):
            for char in garbage[index]:
                mapping[index][char] += 1
                index_maximum[char] = index

        # Option 1
        result = 0
        # M
        result += self.getCollectTimes('M', index_maximum, mapping, travel)

        # P
        result += self.getCollectTimes('P', index_maximum, mapping, travel)

        # G
        result += self.getCollectTimes('G', index_maximum, mapping, travel)
        """
        # Option 2

        result = self.getCollectTimes('M', index_maximum, mapping, travel) + self.getCollectTimes('P', index_maximum, mapping, travel) + self.getCollectTimes('G', index_maximum, mapping, travel)
        """

        return result

    def getCollectTimes(self, char: str, index_maximum: Dict[str, int], mapping: List[Dict[str, int]], travel: List[int]) -> int:
        result = 0
        for index in range(len(mapping)):
            if char not in index_maximum or index_maximum[char] < index:
                break

            if index > 0:
                result += travel[index-1]

            if char in mapping[index]:
                result += mapping[index][char]

        return result
```

Method 3 :
```python
class Solution:
    def garbageCollection(self, garbage: List[str], travel: List[int]) -> int:
        index_maximum = {}
        for index in range(len(garbage)):
            for char in garbage[index]:
                index_maximum[char] = index

        result = self.getCollectTimes('M', index_maximum, garbage, travel) + self.getCollectTimes('P', index_maximum, garbage, travel) + self.getCollectTimes('G', index_maximum, garbage, travel)

        return result

    def getCollectTimes(self, char: str, index_maximum: Dict[str, int], garbage: List[str], travel: List[int]) -> int:
        result = 0
        for index in range(len(garbage)):
            if char not in index_maximum or index_maximum[char] < index:
                break

            if index > 0:
                result += travel[index-1]

            result += garbage[index].count(char)

        return result
```

Method 4 (Prefix Sum) :
```python
class Solution:
    def garbageCollection(self, garbage: List[str], travel: List[int]) -> int:
        counter = defaultdict(int)
        index_maximum = {}
        for index in range(len(garbage)):
            for char in garbage[index]:
                index_maximum[char] = index
                counter[char] += 1

        # Option 1
        prefix_sum = [travel[0]]
        for index in range(1, len(travel)):
            prefix_sum.append(travel[index] + prefix_sum[index-1])
        """
        # Option 2

        n = len(travel)
        prefix_sum = [0] * n
        prefix_sum[0] = travel[0]
        for index in range(1, n):
            prefix_sum[index] = travel[index] + prefix_sum[index-1]
        """

        result = self.getCollectTimes('M', index_maximum, counter, prefix_sum) + self.getCollectTimes('P', index_maximum, counter, prefix_sum) + self.getCollectTimes('G', index_maximum, counter, prefix_sum)

        return result

    def getCollectTimes(self, char: str, index_maximum: Dict[str, int], counter: Dict[str, int], prefix_sum: List[int]) -> int:
        if char not in index_maximum:
            return 0

        return counter[char] + (prefix_sum[index_maximum[char]-1] if index_maximum[char] > 0 else 0)
```

Method 5 (Time Complexity: $O(M*N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def garbageCollection(self, garbage: List[str], travel: List[int]) -> int:
        result = 0
        index_maximum = {}
        for index in range(len(garbage)):
            for char in garbage[index]:
                index_maximum[char] = index
                # Option 1
                result += 1
                """
                # Option 2

            result += len(garbage[index])
                """

        for index in range(1, len(travel)):
            travel[index] += travel[index-1]

        result += self.getCollectTimes('M', index_maximum, travel) + self.getCollectTimes('P', index_maximum, travel) + self.getCollectTimes('G', index_maximum, travel)

        return result

    def getCollectTimes(self, char: str, index_maximum: Dict[str, int], travel: List[int]) -> int:
        if char not in index_maximum or index_maximum[char] == 0:
            return 0

        return travel[index_maximum[char]-1]
```

Method 6 :
```python
class Solution:
    def garbageCollection(self, garbage: List[str], travel: List[int]) -> int:
        result = 0
        index_maximum = [0] * 3
        for index in range(len(garbage)):
            if garbage[index].count('M') > 0:
                index_maximum[0] = index
            if garbage[index].count('P') > 0:
                index_maximum[1] = index
            if garbage[index].count('G') > 0:
                index_maximum[2] = index

            result += len(garbage[index])

        for index in range(1, len(travel)):
            travel[index] += travel[index-1]

        result += self.getCollectTimes(0, index_maximum, travel) + self.getCollectTimes(1, index_maximum, travel) + self.getCollectTimes(2, index_maximum, travel)

        return result

    def getCollectTimes(self, index: int, index_maximum: Dict[str, int], travel: List[int]) -> int:
        if index_maximum[index] is None or index_maximum[index] == 0:
            return 0

        return travel[index_maximum[index]-1]
```

Method 7 :
```python
class Solution:
    def garbageCollection(self, garbage: List[str], travel: List[int]) -> int:
        for index in range(1, len(travel)):
            travel[index] += travel[index-1]

        # Option 1
        result = sum([len(string) for string in garbage])
        """
        # Option 2

        result = len("".join(garbage))
        """
        for char in ["M", "P", "G"]:
            # Option 1
            for index in reversed(range(1, len(garbage))):
            """
            # Option 2

            for index in range(len(garbage)-1, 0, -1):
            """
                if char in garbage[index]:
                    result += travel[index-1]
                    break

        return result
```
