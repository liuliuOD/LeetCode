![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1870. [Minimum Speed To Arrive On Time](https://leetcode.com/problems/minimum-speed-to-arrive-on-time)

### Solution :

Method 1 (Binary Search) :
```python
MAXIMUM = 10**7
class Solution:
    def minSpeedOnTime(self, dist: List[int], hour: float) -> int:
        n = len(dist)
        if hour <= n-1:
            return -1

        speed_left = 1
        speed_right = MAXIMUM
        while speed_left <= speed_right:
            speed = speed_left + (speed_right - speed_left) // 2

            cost = 0
            for index in range(n-1):
                cost += ceil(dist[index]/speed)
            cost += dist[-1] / speed

            if cost <= hour:
                speed_right = speed - 1
            elif cost > hour:
                speed_left = speed + 1
        
        return speed_left
```
