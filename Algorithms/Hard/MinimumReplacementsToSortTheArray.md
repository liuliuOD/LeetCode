![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 2366. [Minimum Replacements To Sort The Array](https://leetcode.com/problems/minimum-replacements-to-sort-the-array)

### Solution :

Method 1 (Greedy) :
```python
class Solution:
    def minimumReplacement(self, nums: List[int]) -> int:
        n = len(nums)
        result = 0
        pointer = n - 1
        later = nums[pointer]
        while pointer > 0:
            pointer -= 1
            current = nums[pointer]

            if later >= current:
                later = current
                continue

            amount_children = (current+later-1) // later # ceil
            later = current // amount_children
            result += amount_children - 1

        return result
```

### Solution :

Method 1 (Greedy) :
```php
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer
     */
    function minimumReplacement($nums) {
        $result = 0;
        $n = count($nums);
        $previous = $nums[$n-1];
        for ($index=$n-2; $index>=0; $index--) {
            $current = $nums[$index];

            if ($current <= $previous) {
                $previous = $current;
                continue;
            }

            $amountChildren = intval(($current+$previous-1) / $previous);
            $previous = intval($current / $amountChildren);
            $result += $amountChildren - 1;
        }

        return $result;
    }
}
```
