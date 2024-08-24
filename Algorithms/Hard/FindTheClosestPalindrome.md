![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 564. [Find The Closest Palindrome](https://leetcode.com/problems/find-the-closest-palindrome)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn nearest_palindromic(num: String) -> String {
        let n: usize = num.len();
        let mut base: i64 = 0;
        for character in num.into_bytes() {
            base = base*10 + (character-b'0') as i64;
        }

        let mut candidates: [i64; 5] = [i64::MAX; 5];
        let mut first: i64 = 0;
        for _ in 0..n-1 {
            first = first*10 + 9;
        }
        candidates[0] = first;

        let mut second: i64 = 10_i64.pow(n as u32) + 1;
        candidates[1] = second;

        let n_half: usize = n / 2;
        let first_half: i64 = base / 10_i64.pow(n_half as u32);

        let mut base_half: i64 = first_half;
        let mut third: i64 = base_half;
        if n%2 == 1 {
            base_half /= 10;
        }
        for _ in 0..n_half {
            third = third*10 + (base_half % 10);
            base_half /= 10;
        }
        candidates[2] = third;

        let mut base_half: i64 = first_half + 1;
        let mut fourth: i64 = base_half;
        if base_half.to_string().len() != (n-n_half) {
            base_half /= 10;
        }
        if n%2 == 1 {
            base_half /= 10;
        }
        for _ in 0..n_half {
            fourth = fourth*10 + (base_half % 10);
            base_half /= 10;
        }
        candidates[3] = fourth;

        let mut base_half: i64 = first_half - 1;
        let mut fifth: i64 = base_half;
        if n%2 == 1 {
            base_half /= 10;
        }
        for _ in 0..n_half {
            fifth = fifth*10 + (base_half % 10);
            base_half /= 10;
        }
        candidates[4] = fifth;

        candidates.sort();

        let mut closest: [i64; 2] = [i64::MAX; 2];
        for value in candidates {
            let distance: i64 = (base - value).abs();
            if value != base && distance < closest[0] {
                closest[0] = distance;
                closest[1] = value;
            }
        }

        return closest[1].to_string()
    }
}
```

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

Method 3 (Binary Search) :
```python
class Solution:
    def nearestPalindromic(self, n: str) -> str:
        n = int(n)
        maximum_palindrom_smaller_than_n = 0
        left = 0
        right = n
        while left < right:
            middle = left + (right - left)//2
            palindrom = self.getPalindromic(middle)
            if palindrom < n:
                maximum_palindrom_smaller_than_n = palindrom
                left = middle + 1
            else:
                right = middle

        minimum_palindrom_larger_than_n = 0
        left = n + 1
        right = 10 ** 18
        while left < right:
            middle = left + (right - left)//2
            palindrom = self.getPalindromic(middle)
            if palindrom > n:
                minimum_palindrom_larger_than_n = palindrom
                right = middle
            else:
                left = middle + 1

        if n - maximum_palindrom_smaller_than_n <= minimum_palindrom_larger_than_n - n:
            return str(maximum_palindrom_smaller_than_n)

        return str(minimum_palindrom_larger_than_n)

    def getPalindromic(self, num: int) -> int:
        num = list(str(num))
        n = len(num)
        left = (n-1) // 2
        right = n // 2
        while left >= 0:
            num[right] = num[left]
            left -= 1
            right += 1

        return int(''.join(num))
```
