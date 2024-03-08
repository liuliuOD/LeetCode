![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 15. [3 Sum](https://leetcode.com/problems/3sum)

### Solution :

Method 1 (Brute Force, ERROR: "Time Limit Exceeded", 309/312) :
```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        n = len(nums)
        mapping = defaultdict(list)
        for index, num in enumerate(nums):
            for index_2 in range(index+1, n):
                mapping[num+nums[index_2]].append([index, index_2])

        result = set()
        for index, num in enumerate(nums):
            for index_1, index_2 in mapping[-num]:
                if index == index_1 or index == index_2:
                    continue

                group = sorted([num, nums[index_1], nums[index_2]])
                result.add(tuple(group))

        return list(result)
```

Method 2 (Hash Map) :
```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        # Option 1
        mapping = defaultdict(int)
        for num in nums:
            mapping[num] += 1
        """
        # Option 2

        mapping = Counter(nums)
        """

        n = len(nums)
        result = set()
        for index_1 in range(n-1):
            num1 = nums[index_1]
            mapping[num1] -= 1
            for index_2 in range(index_1+1, n):
                num2 = nums[index_2]
                mapping[num2] -= 1

                target = -(num1 + num2)
                if target in mapping and mapping[target] > 0:
                    result.add(tuple(sorted([num1, num2, target])))

                mapping[num2] += 1

            mapping[num1] += 1

        return result
```

Method 3 (Two Pointer) :
```python
class Solution:
    def threeSum(self, nums: List[int]) -> List[List[int]]:
        nums.sort()

        n = len(nums)
        result = []
        for index in range(n-1):
            num1 = nums[index]
            if index > 0 and num1 == nums[index-1]:
                continue

            left = index + 1
            right = n - 1
            while left < right:
                num2 = nums[left]
                num3 = nums[right]
                sumCurrent = num1 + num2 + num3
                if sumCurrent == 0:
                    result.append([num1, num2, num3])
                    while left < right and nums[left] == nums[left+1]:
                        left += 1
                    while left < right and nums[right] == nums[right-1]:
                        right -= 1

                    left += 1
                    right -= 1
                elif sumCurrent > 0:
                    right -= 1
                elif sumCurrent < 0:
                    left += 1

        return result
```

### Solution :

Method 1 (Hash Map) :
```php
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer[][]
     */
    function threeSum($nums) {
        $mapping = [];
        foreach($nums as $num) {
            isset($mapping[$num])
                ? $mapping[$num]++
                : $mapping[$num] = 1;
        }

        $n = count($nums);
        $set = [];
        for($index1 = 0; $index1 < $n; $index1++) {
            $num1 = $nums[$index1];
            $mapping[$num1]--;
            for($index2 = $index1+1; $index2 < $n; $index2++) {
                $num2 = $nums[$index2];
                $mapping[$num2]--;

                $target = -($num1 + $num2);
                if (isset($mapping[$target]) && $mapping[$target] > 0) {
                    $temp = [$num1, $num2, $target];
                    sort($temp);
                    $set[implode('+', $temp)] = true;
                }
                $mapping[$num2]++;
            }
            $mapping[$num1]++;
        }

        $result = [];
        foreach(array_keys($set) as $group) {
            $result[] = explode('+', $group);
        }

        return $result;
    }
}
```

Metho 2 (Two Pointer + Array Key, remove duplication) :
```php
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer[][]
     */
    function threeSum($nums) {
        sort($nums);
        $n = count($nums);
        $set = [];
        for($index = 0; $index < $n; $index++) {
            $left = $index + 1;
            $right = $n - 1;
            while ($left < $right) {
                $sum = $nums[$index] + $nums[$left] + $nums[$right];
                if ($sum == 0) {
                    $set["$nums[$index]+$nums[$left]+$nums[$right]"] = true;
                    $right--;
                    $left++;
                } else if ($sum > 0) {
                    $right--;
                } else if ($sum < 0) {
                    $left++;
                }
            }
        }

        $result = [];
        foreach(array_keys($set) as $key) {
            $result[] = explode('+', $key);
        }

        return $result;
    }
}
```

Method 3 (Two Pointer + Loop, skip duplication) :
```php
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer[][]
     */
    function threeSum($nums) {
        sort($nums);
        $n = count($nums);
        $result = [];
        for($index = 0; $index < $n-1; $index++) {
            if ($index > 0 && $nums[$index] == $nums[$index-1]) {
                continue;
            }

            $left = $index + 1;
            $right = $n - 1;
            while ($left < $right) {
                $sum = $nums[$index] + $nums[$left] + $nums[$right];
                if ($sum == 0) {
                    $result[] = [$nums[$index], $nums[$left], $nums[$right]];
                    while ($left < $right && $nums[$left] == $nums[$left+1]) {
                        $left++;
                    }
                    while ($right > $left && $nums[$right] == $nums[$right-1]) {
                        $right--;
                    }
                    $left++;
                    $right--;
                } else if ($sum > 0) {
                    $right--;
                } else if ($sum < 0) {
                    $left++;
                }
            }
        }

        return $result;
    }
}
```
