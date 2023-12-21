![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 564. [Find The Closest Palindrome](https://leetcode.com/problems/find-the-closest-palindrome)

### Solution :

Method 1 (Brute Force, ERROR: "Time Limit Exceeded") :
```python
class Solution:
    def nearestPalindromic(self, n: str) -> str:
        n = int(n)
        smaller = n - 1
        while not self.isPalindromic(smaller):
            smaller -= 1

        larger = n + 1
        while not self.isPalindromic(larger):
            larger += 1

        if larger - n < n - smaller:
            return str(larger)

        return str(smaller)

    def isPalindromic(self, num: int) -> bool:
        num = str(num)
        n = len(num)
        index = n//2 - 1
        offset = 2 if n % 2 == 1 else 1

        while index >= 0:
            if num[index] != num[index+offset]:
                return False

            index -= 1
            offset += 2

        return True
```

Method 2 :
```python
class Solution:
    def nearestPalindromic(self, num: str) -> str:
        n = len(num)
        num_list = list(num)
        half = (n+1) // 2
        num_left = int(''.join(num_list[:half]))
        candidates = [self.getPalindromic(num_left, half, n), self.getPalindromic(num_left+1, half, n), self.getPalindromic(num_left-1, half, n)]

        num_int = int(num)
        result = (-inf, inf)
        for candidate in sorted(candidates):
            difference = abs(candidate - num_int)
            if 0 < difference < result[1]:
                result = (candidate, difference)

        return str(result[0])

    def getPalindromic(self, num: int, n_half: int, n: int) -> int:
        if num == 0:
            if n == 1:
                return 0
            return 9

        # left half => 99
        if len(str(num)) > n_half:
            return int("1"+"0"*(n-1)+"1")
        # left half => 100
        if len(str(num)) < n_half:
            return int("9"*(n-1))

        temp = num
        candidates = []
        while num:
            candidates.append(num%10)
            num //= 10

        for index in range(n%2, n-n_half+(1 if n % 2 else 0)):
            temp = temp * 10 + candidates[index]

        return temp
```
