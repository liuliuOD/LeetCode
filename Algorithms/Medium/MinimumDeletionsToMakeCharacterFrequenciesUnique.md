![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 1647. [Minimum Deletions To Make Character Frequencies Unique](https://leetcode.com/problems/minimum-deletions-to-make-character-frequencies-unique)

### Solution :

Method 1 (Hash Set) :
```python
class Solution:
    def minDeletions(self, s: str) -> int:
        frequency = Counter(s)
        existed = set()
        result = 0

        for value in frequency.values():
            while value > 0 and value in existed:
                value -= 1
                result += 1

            existed.add(value)

        return result
```

### Solution :

Method 1 (Brute Force) :
```php
class Solution {

    /**
     * @param String $s
     * @return Integer
     */
    function minDeletions($s) {
        $mapping = [];
        foreach (str_split($s) as $char) {
            if (!isset($mapping[$char])) {
                $mapping[$char] = 0;
            }

            $mapping[$char]++;
        }

        $frequency = array_values($mapping);
        rsort($frequency);
        $n = count($frequency);
        $result = 0;
        for ($indexLeft = 0; $indexLeft < $n; $indexLeft++) {
            for ($indexRight = $indexLeft+1; $indexRight < $n; $indexRight++) {
                if (
                    ($frequency[$indexLeft] != $frequency[$indexRight])
                    || $frequency[$indexRight] == 0
                ) {
                    continue;
                }

                $frequency[$indexRight]--;
                $result++;
            }
        }

        return $result;
    }
}
```

Method 2 (Hash Set) :
```php
class Solution {

    /**
     * @param String $s
     * @return Integer
     */
    function minDeletions($s) {
        $mapping = [];
        foreach (str_split($s) as $char) {
            if (!isset($mapping[$char])) {
                $mapping[$char] = 0;
            }

            $mapping[$char]++;
        }

        $frequency = array_values($mapping);
        $set = [];
        $result = 0;
        foreach ($frequency as $value) {
            while (isset($set[$value])) {
                $value--;
                $result++;
            }

            if ($value > 0) {
                $set[$value] = true;
            }
        }

        return $result;
    }
}
```
