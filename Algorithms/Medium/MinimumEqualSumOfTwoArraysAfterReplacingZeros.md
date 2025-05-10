![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2918. [Minimum Equal Sum Of Two Arrays After Replacing Zeros](https://leetcode.com/problems/minimum-equal-sum-of-two-arrays-after-replacing-zeros)

### Solution :

Method 1 (Greedy, Time Complexity: $O(M+N)$, Space Complexity: $O(1)$ (M: the number of elements in `nums1`, N: the number of elements in `nums2`)) :
```rust
impl Solution {
    pub fn min_sum(nums1: Vec<i32>, nums2: Vec<i32>) -> i64 {
        let mut sum_1: i64 = nums1.iter().map(|num| *num as i64).sum();
        let mut sum_2: i64 = nums2.iter().map(|num| *num as i64).sum();
        let amount_zero_1: i64 = nums1.iter().filter(|&num| *num == 0).count() as i64;
        let amount_zero_2: i64 = nums2.iter().filter(|&num| *num == 0).count() as i64;
        sum_1 += amount_zero_1;
        sum_2 += amount_zero_2;

        if (sum_1 < sum_2 && amount_zero_1 > 0) ||
            (sum_1 == sum_2) {
            return sum_2
        } else if sum_1 > sum_2 && amount_zero_2 > 0 {
            return sum_1
        }
        return -1
    }
}
```

### Solution :

Method 1 (In weekly contest 369) :
```python
class Solution:
    def minSum(self, nums1: List[int], nums2: List[int]) -> int:
        sum1 = sum2 = 0
        amount_zero1 = amount_zero2 = 0
        for num1 in nums1:
            if num1 == 0:
                amount_zero1 += 1
            else:
                sum1 += num1
        for num2 in nums2:
            if num2 == 0:
                amount_zero2 += 1
            else:
                sum2 += num2

        temp1 = sum1 + amount_zero1
        temp2 = sum2 + amount_zero2
        result = temp1
        if temp1 > temp2:
            if amount_zero2 == 0:
                return -1

            result = temp1
        elif temp1 < temp2:
            if amount_zero1 == 0:
                return -1

            result = temp2

        return result
```

Method 2 :
```python
class Solution:
    def minSum(self, nums1: List[int], nums2: List[int]) -> int:
        amount_zero1 = nums1.count(0)
        amount_zero2 = nums2.count(0)
        sum1 = sum(nums1) + amount_zero1
        sum2 = sum(nums2) + amount_zero2

        if sum1 > sum2 and amount_zero2 == 0:
            return -1
        elif sum1 < sum2 and amount_zero1 == 0:
            return -1

        return max(sum1, sum2)
```
