![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 125. [Valid Palindrome](https://leetcode.com/problems/valid-palindrome)

### Solution :

Method 1 (Regex + Two Pointer) :
```python
import re

class Solution:
    def isPalindrome(self, s: str) -> bool:
        s = re.sub(r'[^a-zA-Z\d]', '', s).lower()
        left = 0
        right = len(s) - 1
        while left < right:
            if s[left] != s[right]:
                return False

            left += 1
            right -= 1

        return True
```

### Solution :

Method 1 (Regex + Two Pointer) :
```php
class Solution {

    /**
     * @param String $s
     * @return Boolean
     */
    function isPalindrome($s) {
        $s = preg_replace('/[^a-zA-Z\d]/', '', $s);
        $s = strtolower($s);

        $left = 0;
        $right = strlen($s) - 1;
        while ($left < $right) {
            if ($s[$left++] != $s[$right--]) {
                return false;
            }
        }

        return true;
    }
}
```

Method 2 (Two Pointer) :
```php
class Solution {

    /**
     * @param String $s
     * @return Boolean
     */
    function isPalindrome($s) {
        $n = strlen($s);
        $left = 0;
        $right = $n - 1;
        while ($left < $right) {
            $charLeft = $s[$left];
            $charRight = $s[$right];
            while ($left < $n && !is_numeric($charLeft) && !ctype_alpha($charLeft)){
                $charLeft = $s[++$left];
            }
            while ($right >= 0 && !is_numeric($charRight) && !ctype_alpha($charRight)){
                $charRight = --$right >= 0
                    ? $s[$right]
                    : '';
            }

            if (strtolower($charLeft) != strtolower($charRight)) {
                return false;
            }

            $left++;
            $right--;
        }

        return true;
    }
}
```

Method 3 :
```php
class Solution {

    /**
     * @param String $s
     * @return Boolean
     */
    function isPalindrome($s) {
        $n = strlen($s);
        $left = 0;
        $right = $n - 1;
        while ($left < $right) {
            $charLeft = $s[$left];
            $charRight = $s[$right];

            # Option 1
            if (!is_numeric($charLeft) && !ctype_alpha($charLeft)){
                $left++;
            } else if (!is_numeric($charRight) && !ctype_alpha($charRight)){
                $right--;
            } else {
                if (strtolower($charLeft) != strtolower($charRight)) {
                    return false;
                }

                $left++;
                $right--;
            }
            /**
             * # Option 2
             * 
             * $left++;
             * if (!is_numeric($charLeft) && !ctype_alpha($charLeft)){
             *     continue;
             * }
             * 
             * $right--;
             * if (!is_numeric($charRight) && !ctype_alpha($charRight)){
             *     $left--;
             *     continue;
             * }
             * 
             * if (strtolower($charLeft) != strtolower($charRight)) {
             *     return false;
             * }
             */
        }

        return true;
    }
}
```
