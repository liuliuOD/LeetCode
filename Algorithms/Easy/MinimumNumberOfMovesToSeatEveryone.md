![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2037. [Minimum Number Of Moves To Seat Everyone](https://leetcode.com/problems/minimum-number-of-moves-to-seat-everyone)

### Solution :

Method 1 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minMovesToSeat(self, seats: List[int], students: List[int]) -> int:
        seats.sort()
        students.sort()
        result = 0
        n = len(seats)
        for index in range(n):
            result += abs(seats[index]-students[index])

        return result
```
