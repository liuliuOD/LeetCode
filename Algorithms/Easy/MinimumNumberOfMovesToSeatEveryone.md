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

Method 2 (Counting Sort, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minMovesToSeat(self, seats: List[int], students: List[int]) -> int:
        seats = self.counting_sort(seats)
        students = self.counting_sort(students)
        result = 0
        n = len(seats)
        for index in range(n):
            result += abs(seats[index]-students[index])

        return result

    def counting_sort(self, nums: list[int]) -> list[int]:
        counter = [0] * 101
        for num in nums:
            counter[num] += 1

        result = [0] * len(nums)
        index = 0
        for num in range(1, 101):
            amount = counter[num]
            result[index:index+amount] = [num] * amount
            index += amount

        return result
```

Method 3 (Radix Sort, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minMovesToSeat(self, seats: List[int], students: List[int]) -> int:
        seats = self.radix_sort(seats)
        students = self.radix_sort(students)
        result = 0
        n = len(seats)
        for index in range(n):
            result += abs(seats[index]-students[index])

        return result

    def radix_sort(self, nums: list[int]) -> list[int]:
        for bit in range(7):
            nums = self.bucket_sort(nums, bit)

        return nums

    def bucket_sort(self, nums: list[int], bit: int) -> list[int]:
        buckets = [[] for _ in range(2)]
        for num in nums:
            buckets[(num >> bit) & 1].append(num)

        result = []
        for group in buckets:
            result.extend(group)

        return result
```
