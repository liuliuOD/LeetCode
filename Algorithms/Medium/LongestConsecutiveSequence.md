![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 128. [Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence)

### Constraints:

- You must write an algorithm that runs in $O(N)$ time.

### Solution :

Method 1 (Time Complexity: $O(N)$) :
```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        mapping = {}
        for num in nums:
            mapping[num] = True

        # only the start of sequence be set to True, and remaining be set to False
        for num in nums:
            if num-1 in mapping:
                mapping[num] = False

        result = 0
        for num in nums:
            # skip following steps if `num`` is not start of a sequence
            if mapping[num] is False:
                continue

            offset = 0
            counter = 0
            while num+offset in mapping:
                counter += 1
                offset += 1

            result = max(result, counter)

        return result
```

Method 2 (Time Complexity: $O(N)$) :
```python
class Solution:
    def longestConsecutive(self, nums: List[int]) -> int:
        visited = set()
        mapping = {}
        result = 0
        for num in nums:
            if num in visited:
                continue
            visited.add(num)

            left = right = num
            if num-1 in visited:
                left_previous, _ = mapping[num-1]
                left = left_previous
            if num+1 in visited:
                _, right_next = mapping[num+1]
                right = right_next

            mapping[left] = mapping[right] = [left, right]
            result = max(result, right-left+1)

        return result
```

### Solution :

Method 1 (Time Complexity: $O(N)$) :
```php
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer
     */
    function longestConsecutive($nums) {
        $mapping = [];
        foreach ($nums as $num) {
            $mapping[$num] = true;
        }

        foreach ($nums as $num) {
            if (isset($mapping[$num-1])) {
                $mapping[$num] = false;
            }
        }

        $result = 0;
        foreach ($nums as $num) {
            if ($mapping[$num] == false) {
                continue;
            }

            $offset = 0;
            while (isset($mapping[$num+$offset])) {
                $offset++;
            }

            $result = max($result, $offset);
        }

        return $result;
    }
}
```

Method 2 (Time Complexity: $O(N)$) :
```php
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer
     */
    function longestConsecutive($nums) {
        $result = 0;
        $mapping = [];
        $visited = [];
        foreach ($nums as $num) {
            if (isset($visited[$num])) {
                continue;
            }
            $visited[$num] = true;

            $left = $right = $num;
            if (isset($mapping[$num-1])) {
                list($left, $_) = $mapping[$num-1];
            }
            if (isset($mapping[$num+1])) {
                list($_, $right) = $mapping[$num+1];
            }

            $mapping[$left] = $mapping[$right] = [$left, $right];

            $result = max($result, $right-$left+1);
        }

        return $result;
    }
}
```
