![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2141. [Maximum Running Time Of N Computers](https://leetcode.com/problems/maximum-running-time-of-n-computers)

### Solution :

Method 1 (Heap, ERROR: "Time Limit Exceeded", 23/52) :
```python
class Solution:
    def maxRunTime(self, n: int, batteries: List[int]) -> int:
        batteries = [-value for value in batteries]
        heapq.heapify(batteries)

        result = 0
        while len(batteries) >= n:
            using_batteries = []
            for _ in range(n):
                remaining_power = heapq.heappop(batteries) + 1
                if remaining_power == 0:
                    continue
                using_batteries.append(remaining_power)

            for battery in using_batteries:
                heapq.heappush(batteries, battery)

            result += 1

        return result
```

Method 2 (Heap, Want to reduce loop times, ERROR: "Time Limit Exceeded", 22/52) :
```python
class Solution:
    def maxRunTime(self, n: int, batteries: List[int]) -> int:
        batteries = [self.reverse(value) for value in batteries]
        heapq.heapify(batteries)

        result = 0
        while len(batteries) >= n:
            using_batteries = []
            for _ in range(n):
                remaining_power = heapq.heappop(batteries)
                using_batteries.append(self.reverse(remaining_power))

            can_use = minimum_using = using_batteries[-1]
            if batteries:
                maximum_remaining = self.reverse(batteries[0])
                can_use = minimum_using - maximum_remaining + 1

            result += can_use
            for battery in using_batteries:
                remaining_power = battery - can_use
                if remaining_power == 0:
                    continue
                heapq.heappush(batteries, self.reverse(remaining_power))

        return result

    def reverse(self, value: int) -> int:
        return -value
```

Method 3 (Binary Search) :
```python
class Solution:
    def maxRunTime(self, n: int, batteries: List[int]) -> int:
        pointer_left = 1
        pointer_right = sum(batteries) // n

        while pointer_left <= pointer_right:
            middle = pointer_left + (pointer_right-pointer_left) // 2

            if self.valid(middle, n, batteries):
                pointer_left = middle + 1
            else:
                pointer_right = middle - 1

        return pointer_right

    def valid(self, expect_running_time: int, n: int, batteries: List[int]) -> bool:
        actual_running_time = 0
        for battery in batteries:
            actual_running_time += min(battery, expect_running_time)

        return (actual_running_time//n) >= expect_running_time
```
