![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 3153. [Sum Of Digit Differences Of All Pairs](https://leetcode.com/problems/sum-of-digit-differences-of-all-pairs)

### Solution :

Method 1 (In weekly contest 398, Time Complexity: $O(N*D)$ (N: length of `nums`, D: the number of digits, since it is bounded by a constant (at most 10), we can say it is $O(N)$), Space Complexity: $O(N*D)$ (same with the time complexity, $O(N)$)) :
```python
class Solution:
    def sumDigitDifferences(self, nums: List[int]) -> int:
        # by number of digits
        # calculate frequency of numbers
        counter = defaultdict(lambda: defaultdict(int))
        for num in nums:
            index_digit = 0
            while num > 0:
                counter[index_digit][num%10] += 1
                num //= 10
                index_digit += 1

        result = 0
        n = len(counter)
        for index_digit in range(n):
            counter_current = counter[index_digit]
            for number1, number2 in combinations(counter_current.keys(), 2):
                result += counter_current[number1] * counter_current[number2]

        return result
```
Method 2 (Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def sumDigitDifferences(self, nums: List[int]) -> int:
        counter = defaultdict(lambda: defaultdict(int))
        for num in nums:
            index_digit = 0
            while num > 0:
                counter[index_digit][num%10] += 1
                num //= 10
                index_digit += 1

        result = 0
        n = len(counter)
        for index_digit in range(n):
            counter_current = counter[index_digit]
            for number in counter_current.keys():
                result += counter_current[number] * (len(nums)-counter_current[number])

        return result // 2
```
