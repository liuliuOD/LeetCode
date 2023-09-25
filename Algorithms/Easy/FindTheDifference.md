![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 389. [Find The Difference](https://leetcode.com/problems/find-the-difference)

### Solution :

Method 1 (ASCII) :
```python
class Solution:
    def findTheDifference(self, s: str, t: str) -> str:
        return chr(sum([ord(char) for char in t]) - sum([ord(char) for char in s]))
```

Method 2 (Hash Map) :
```python
class Solution:
    def findTheDifference(self, s: str, t: str) -> str:
        mapping = Counter(s)
        for char in t:
            if char not in mapping:
                return char

            mapping[char] -= 1
            if mapping[char] < 0:
                return char
```

Method 3 (Bitwise XOR) :
```python
class Solution:
    def findTheDifference(self, s: str, t: str) -> str:
        result = 0
        for char in s:
            result ^= ord(char)

        for char in t:
            result ^= ord(char)

        return chr(result)
```

### Solution:

Method 1 (Hash Map) :
```php
class Solution {

    /**
     * @param String $s
     * @param String $t
     * @return String
     */
    function findTheDifference($s, $t) {
        $mapping = [];
        foreach(str_split($s) as $char) {
            isset($mapping[$char])
                ? $mapping[$char]++
                : $mapping[$char] = 1;
        }
        foreach(str_split($t) as $char) {
            if (!isset($mapping[$char])) {
                return $char;
            }
            $mapping[$char]--;
            if ($mapping[$char] < 0) {
                return $char;
            }
        }
    }
}
```

Method 2 (ASCII) :
```php
class Solution {

    /**
     * @param String $s
     * @param String $t
     * @return String
     */
    function findTheDifference($s, $t) {
        $n = strlen($s);
        $ascii = ord($t[$n]);
        for ($index = 0; $index < $n; $index++) {
            $ascii += ord($t[$index]) - ord($s[$index]);
        }

        return chr($ascii);
    }
}
```
