![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 11. [Container With Most Water](https://leetcode.com/problems/container-with-most-water)

### Solution :

Method 1 (Two Pointer) :
```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        n = len(height)
        left = 0
        right = n - 1
        result = 0
        while left < right:
            result = max(result, min(height[left], height[right])*(right-left))

            if height[left] > height[right]:
                right -= 1
            else:
                left += 1
        return result
```

### Solution :

Method 1 (Two Pointer) :
```php
class Solution {

    /**
     * @param Integer[] $height
     * @return Integer
     */
    function maxArea($height) {
        $result = 0;

        $left = 0;
        $right = count($height) - 1;
        while ($left < $right) {
            $result = max($result, min($height[$left], $height[$right])*($right-$left));

            $height[$left] > $height[$right]
                ? $right--
                : $left++;
        }

        return $result;
    }
}
```
