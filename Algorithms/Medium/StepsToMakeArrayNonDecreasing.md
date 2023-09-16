![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 2289. [Steps To Make Array Non-decreasing](https://leetcode.com/problems/steps-to-make-array-non-decreasing)

### Solution :

Method 1 (Monotonic Stack) :
```php
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer
     */
    function totalSteps($nums) {
        $n = count($nums);
        $stack = [[end($nums), 0]];
        $result = 0;
        for ($index = $n-2; $index >= 0; $index--) {
            $step = 0;
            while (count($stack) && $nums[$index] > end($stack)[0]) {
                list($_, $stepInStack) = array_pop($stack);
                $step = max($step+1, $stepInStack);
            }

            $stack[] = [$nums[$index], $step];
            $result = max($result, $step);
        }

        return $result;
    }
}
```
