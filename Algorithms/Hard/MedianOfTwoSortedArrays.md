![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
---

## 4. [Median Of Two Sorted Arrays](https://leetcode.com/problems/median-of-two-sorted-arrays)

### Constraints:

- The overall run time complexity should be $O(log(M+N))$.

### Solution :

Method 1 (Merge Array, Time Complexity: $O((M+N)*log(M+N))$) :
```python
class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        nums_merged = nums1 + nums2
        nums_merged.sort()

        index = len(nums_merged) // 2
        return nums_merged[index] if len(nums_merged) % 2 == 1 else (nums_merged[index] + nums_merged[index-1]) / 2
```

Method 2 (Two Pointer, Time Complexity: $O(M+N)$) :
```python
class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        m, n = len(nums1), len(nums2)

        pointer_1 = pointer_2 = 0
        middle_1 = middle_2 = 0
        for _ in range((m+n)//2+1):
            middle_1 = middle_2
            if pointer_1 < m and pointer_2 < n:
                if nums1[pointer_1] > nums2[pointer_2]:
                    middle_2 = nums2[pointer_2]
                    pointer_2 += 1
                else:
                    middle_2 = nums1[pointer_1]
                    pointer_1 += 1
            elif pointer_1 < m:
                middle_2 = nums1[pointer_1]
                pointer_1 += 1
            elif pointer_2 < n:
                middle_2 = nums2[pointer_2]
                pointer_2 += 1

        return (middle_1+middle_2) / 2 if (m+n) % 2 == 0 else middle_2
```

Method 3 (Binary Search, Time Complexity: $O(log(min(M, N)))$) :
```python
class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        m, n = len(nums1), len(nums2)
        # always let m <= n
        if m > n:
            m, n = n, m
            nums1, nums2 = nums2, nums1

        amount_median = (m + n + 1) // 2
        left, right = 0, m
        while left <= right:
            index_partition_nums1 = left + (right - left) // 2
            index_partition_nums2 = amount_median - index_partition_nums1

            min_right_nums1 = float('inf') if index_partition_nums1 == m else nums1[index_partition_nums1]
            max_left_nums1 = float('-inf') if index_partition_nums1 == 0 else nums1[index_partition_nums1-1]

            min_right_nums2 = float('inf') if index_partition_nums2 == n else nums2[index_partition_nums2]
            max_left_nums2 = float('-inf') if index_partition_nums2 == 0 else nums2[index_partition_nums2-1]

            if max_left_nums2 <= min_right_nums1 and max_left_nums1 <= min_right_nums2:
                if (m+n)%2 == 0:
                    return (max(max_left_nums1, max_left_nums2) + min(min_right_nums1, min_right_nums2)) / 2
                else:
                    return max(max_left_nums1, max_left_nums2)
            elif max_left_nums1 > min_right_nums2:
                right = index_partition_nums1 - 1
            elif max_left_nums2 > min_right_nums1:
                left = index_partition_nums1 + 1
```

### Solution :

Method 1 ([Binary Search](https://leetcode.com/problems/median-of-two-sorted-arrays/solutions/4070924/98-33-easy-solution-with-explanation-2-approaches/?envType=daily-question&envId=2023-09-21)) :
```php
class Solution {

    /**
     * @param Integer[] $nums1
     * @param Integer[] $nums2
     * @return Float
     */
    function findMedianSortedArrays($nums1, $nums2) {
        $m = count($nums1);
        $n = count($nums2);
        if ($m > $n) {
            list($nums1, $nums2) = [$nums2, $nums1];
            list($m, $n) = [$n, $m];
        }

        $amountMedian = intval(($m+$n+1) / 2);
        $left = 0;
        $right = $m;
        while($left <= $right) {
            $indexPartition1 = $left + intval(($right-$left)/2);
            $indexPartition2 = $amountMedian - $indexPartition1;

            $maxLeft1 = $indexPartition1 == 0
                ? PHP_INT_MIN
                : $nums1[$indexPartition1-1];
            $minRight1 = $indexPartition1 == $m
                ? PHP_INT_MAX
                : $nums1[$indexPartition1];
            $maxLeft2 = $indexPartition2 == 0
                ? PHP_INT_MIN
                : $nums2[$indexPartition2-1];
            $minRight2 = $indexPartition2 == $n
                ? PHP_INT_MAX
                : $nums2[$indexPartition2];

            if ($maxLeft1 <= $minRight2 && $minRight1 >= $maxLeft2) {
                if (($m+$n)%2) {
                    return max($maxLeft1, $maxLeft2);
                }

                return (max($maxLeft1, $maxLeft2) + min($minRight1, $minRight2)) / 2;
            } else if ($maxLeft1 > $minRight2) {
                $right = $indexPartition1 - 1;
            } else if ($minRight1 < $maxLeft2) {
                $left = $indexPartition1 + 1;
            }
        }
    }
}
```
