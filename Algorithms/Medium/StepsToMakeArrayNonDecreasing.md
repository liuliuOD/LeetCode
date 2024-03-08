![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 2289. [Steps To Make Array Non-decreasing](https://leetcode.com/problems/steps-to-make-array-non-decreasing)

### Solution :

Method 1 (Monotonic Stack) :
```python
class Solution:
    def totalSteps(self, nums: List[int]) -> int:
        n = len(nums)
        stack = []
        index = n - 1
        result = 0
        while index >= 0:
            steps = 0
            while stack and stack[-1][0] < nums[index]:
                steps = max(steps+1, stack.pop()[1])

            result = max(result, steps)
            stack.append((nums[index], steps))
            index -= 1

        return result
```

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
