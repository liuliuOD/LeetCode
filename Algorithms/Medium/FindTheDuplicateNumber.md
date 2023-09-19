![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 287. [Find The Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number)

### Constraints:

- Solve the problem without modifying the array `num`.
- Uses only constant extra space.

### Solution :

Method 1 (Binary Search) :
```python
class Solution:
    def findDuplicate(self, nums: List[int]) -> int:
        n = len(nums)
        left = 1
        right = n - 1
        while left <= right:
            middle = left + (right - left)//2

            amount = 0
            for num in nums:
                if num <= middle:
                    amount += 1

            if amount <= middle:
                left = middle + 1
            else:
                right = middle - 1

        return left
```

### Solution :

Method 1 (Binary Search) :
```php
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer
     */
    function findDuplicate($nums) {
        $n = count($nums);
        $left = 1;
        $right = $n - 1;
        while ($left <= $right) {
            $middle = $left + intval(($right - $left) / 2);

            $amount = 0;
            foreach($nums as $num) {
                if ($num <= $middle) {
                    $amount++;
                }
            }

            if ($amount <= $middle) {
                $left = $middle + 1;
            } else {
                $right = $middle - 1;
            }
        }

        return $left;
    }
}
```

Method 2 (Bitwise) :
```php
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer
     */
    function findDuplicate($nums) {
        $bitsNums = $bitsN = array_fill(0, 32, 0);
        foreach($nums as $num) {
            for ($offset = 0; $offset < 32; $offset++) {
                if ($num & (1<<$offset)) {
                    $bitsNums[$offset]++;
                }
            }
        }

        for($num = 1; $num < count($nums); $num++) {
            for ($offset = 0; $offset < 32; $offset++) {
                if ($num & (1<<$offset)) {
                    $bitsN[$offset]++;
                }
            }
        }

        $result = 0;
        for($offset = 0; $offset < 32; $offset++) {
            if ($bitsN[$offset] < $bitsNums[$offset]) {
                $result |= (1<<$offset);
            }
        }

        return $result;
    }
}
```

Method 3 (Bitwise) :
```php
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer
     */
    function findDuplicate($nums) {
        $bitsNums = $bitsN = array_fill(0, 32, 0);
        foreach($nums as $num) {
            $offset = 0;
            while ($num) {
                if ($num % 2) {
                    $bitsNums[$offset]++;
                }
                $num = intval($num / 2);
                $offset++;
            }
        }

        for($num = 1; $num < count($nums); $num++) {
            $offset = 0;
            $temp = $num;
            while ($temp) {
                if ($temp % 2) {
                    $bitsN[$offset]++;
                }
                $temp = intval($temp / 2);
                $offset++;
            }
        }

        $result = 0;
        for($offset = 0; $offset < 32; $offset++) {
            if ($bitsN[$offset] < $bitsNums[$offset]) {
                $result |= (1<<$offset);
            }
        }

        return $result;
    }
}
```
