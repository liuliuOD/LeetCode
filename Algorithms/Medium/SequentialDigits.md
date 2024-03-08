![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1291. [Sequential Digits](https://leetcode.com/problems/sequential-digits)

### Solution :

Method 1 (Hash Set, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def sequentialDigits(self, low: int, high: int) -> List[int]:
        digit_low = len(str(low))
        digit_high = len(str(high))
        result = set()
        for start in range(1, 10):
            for digit in range(digit_low, digit_high+1):
                current = start
                temp = 0
                while digit and 1 <= current <= 9:
                    digit -= 1
                    temp = temp * 10 + current
                    current += 1

                if temp < low or temp > high:
                    continue

                result.add(temp)

        return sorted(list(result))
```

Method 2 (Sliding Window, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
BASE: str = "123456789"
class Solution:
    def sequentialDigits(self, low: int, high: int) -> List[int]:
        window_start = len(str(low))
        window_end = len(str(high))
        result = []
        for window in range(window_start, window_end+1):
            for index in range(9-window+1):
                num = int(BASE[index:index+window])
                if num < low or num > high:
                    continue

                result.append(num)

        return result
```

Method 3 (Sliding Window, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
BASE: str = "123456789"
class Solution:
    def sequentialDigits(self, low: int, high: int) -> List[int]:
        window_start = len(str(low))
        window_end = len(str(high))
        result = []
        for index in range(9):
            for window in range(window_start, window_end+1):
                if index+window > 9:
                    break

                num = int(BASE[index:index+window])
                if num < low or num > high:
                    continue

                result.append(num)

        return sorted(result)
```
