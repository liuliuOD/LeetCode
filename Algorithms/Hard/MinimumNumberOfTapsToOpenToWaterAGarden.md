![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/%20-PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 1326. [Minimum Number Of Taps To Open To Water A Garden](https://leetcode.com/problems/minimum-replacements-to-sort-the-array)

### Solution :

Method 1 (Greedy) :
```python
class Solution:
    def minTaps(self, n: int, ranges: List[int]) -> int:
        tap_ranges = list(range(n+1))
        for index, offset in enumerate(ranges):
            if offset == 0:
                continue

            side_left = max(0, index - offset)
            side_right = index + offset
            tap_ranges[side_left] = max(tap_ranges[side_left], side_right)

        result, end_previous_choose, end_farthest = 0, 0, 0
        for index in range(len(tap_ranges)):
            # if there is a watered gap, like [0, 2] and [3, 5], it is invalid
            if index > end_previous_choose >= end_farthest:
                return -1

            # end_farthest > end_previous_choose means we need to choose another tap to water the dry field
            if index > end_previous_choose:
                result += 1
                end_previous_choose = end_farthest

            # add range of current tap into end_farthest at the last step to prevent a watered gap
            end_farthest = max(end_farthest, tap_ranges[index])

        return result
```

Method 2 (Dynamic Programming) :
```python
```

### Solution :

Method 1 (Greedy) :
```php
class Solution {

    /**
     * @param Integer $n
     * @param Integer[] $ranges
     * @return Integer
     */
    function minTaps($n, $ranges) {
        $tapRanges = array_fill(0, count($ranges), 0);
        foreach($ranges as $index => $range) {
            if ($range == 0) {
                continue;
            }

            $key = max(0, $index-$range);
            $tapRanges[$key] = max($tapRanges[$key], $index+$range);
        }

        $result = $endChoose = $endFarthest = 0;
        for ($index=0; $index < count($tapRanges); $index++) {
            if ($index > $endChoose && $endChoose >= $endFarthest) {
                return -1;
            }

            if ($index > $endChoose) {
                $result++;
                $endChoose = $endFarthest;
            }

            $endFarthest = max($endFarthest, $tapRanges[$index]);
        }

        return $result;
    }
}
```
