![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 2825. [Make String A Subsequence Using Cyclic Increments](https://leetcode.com/problems/make-string-a-subsequence-using-cyclic-increments)

### Solution :

Method 1 (Two Pointers) :
```python
class Solution:
    def canMakeSubsequence(self, str1: str, str2: str) -> bool:
        len_1 = len(str1)
        len_2 = len(str2)
        if len_2 > len_1:
            return False

        pointer_1 = pointer_2 = 0
        while pointer_1 < len_1 and pointer_2 < len_2:
            if str1[pointer_1] == str2[pointer_2]:
                pointer_1 += 1
                pointer_2 += 1
                continue

            char = chr(ord(str1[pointer_1])+1) if ord(str1[pointer_1])+1 <= ord('z') else 'a'
            if char == str2[pointer_2]:
                pointer_2 += 1

            pointer_1 += 1
        return pointer_2 >= len_2
```

Method 2 (Two Pointers) :
```python
class Solution:
    def canMakeSubsequence(self, str1: str, str2: str) -> bool:
        len_1 = len(str1)
        len_2 = len(str2)
        if len_2 > len_1:
            return False

        pointer_1 = pointer_2 = 0
        while pointer_1 < len_1 and pointer_2 < len_2:
            if (str1[pointer_1] == str2[pointer_2]) or (ord(str1[pointer_1])-ord(str2[pointer_2]) == -1) or (str1[pointer_1] == 'z' and str2[pointer_2] == 'a'):
                pointer_2 += 1

            pointer_1 += 1

        return pointer_2 >= len_2
```

### Solution :

Method 1 (Two Pointers) :
```php
class Solution {

    /**
     * @param String $str1
     * @param String $str2
     * @return Boolean
     */
    function canMakeSubsequence($str1, $str2) {
        $len1 = strlen($str1);
        $len2 = strlen($str2);
        if ($len2 > $len1) {
            return false;
        }

        $pointer1 = $pointer2 = 0;
        while ($pointer1 < $len1 && $pointer2 < $len2) {
            $char1 = $str1[$pointer1];
            $char2 = $str2[$pointer2];
            $pointer1++;
            if (
                ($char1 === $char2)
                || ($char1 === 'z' && $char2 === 'a')
                || (++$char1 === $char2) // $char1 has been modified
            ) {
                $pointer2++;
            }
        }

        return $pointer2 >= $len2;
    }
}
```
