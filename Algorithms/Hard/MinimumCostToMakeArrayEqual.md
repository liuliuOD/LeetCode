![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2448. [Minimum Cost To Make Array Equal](https://leetcode.com/problems/minimum-cost-to-make-array-equal)

### Solution :

Method 1 (Binary Search) :
```rust
impl Solution {
    pub fn min_cost(nums: Vec<i32>, cost: Vec<i32>) -> i64 {
        let mut result: i64 = -1;
        let mut minimum: i32 = 1;
        let mut maximum: i32 = (10 as i32).pow(6);
        while minimum <= maximum {
            let middle: i32 = minimum + (maximum - minimum) / 2;
            let mut total_cost_middle_floor = 0;
            let mut total_cost_middle_ceil = 0;
            for (index, num) in nums.iter().enumerate() {
                total_cost_middle_floor += (middle-num).abs() as i64 * cost[index] as i64;
                total_cost_middle_ceil += ((middle+1)-num).abs() as i64 * cost[index] as i64;
            }

            if result < 0 {
                result = *[total_cost_middle_floor, total_cost_middle_ceil].iter().min().unwrap();
            }
            else {
                result = *[result, total_cost_middle_floor, total_cost_middle_ceil].iter().min().unwrap();
            }

            if total_cost_middle_floor < total_cost_middle_ceil {
                maximum = middle - 1;
            }
            else {
                minimum = middle + 1;
            }
        }
        return result
    }
}
```

Method 2 (Binary Search) :
```rust
impl Solution {
    pub fn min_cost(nums: Vec<i32>, cost: Vec<i32>) -> i64 {
        let mut result: i64 = -1;
        let mut minimum: i32 = 1;
        let mut maximum: i32 = (10 as i32).pow(6);

        while minimum <= maximum {
            let middle: i32 = minimum + (maximum - minimum) / 2;
            let (total_cost_middle_floor, total_cost_middle_ceil) = Self.total_cost_sum(&nums, &cost, middle);

            if result < 0 {
                result = *[total_cost_middle_floor, total_cost_middle_ceil].iter().min().unwrap();
            }
            else {
                result = *[result, total_cost_middle_floor, total_cost_middle_ceil].iter().min().unwrap();
            }

            if total_cost_middle_floor < total_cost_middle_ceil {
                maximum = middle - 1;
            }
            else {
                minimum = middle + 1;
            }
        }
        return result
    }

    fn total_cost_sum(&self, nums: &Vec<i32>, cost: &Vec<i32>, middle: i32) -> (i64, i64) {
        let calculate_cost = |mid: i32| -> i64 {
            return nums.iter().zip(cost.iter()).map(|(&num, &num_cost)| {
                (mid-num).abs() as i64 * num_cost as i64
            }).sum()
        };

        return (calculate_cost(middle), calculate_cost(middle+1))
    }
}
```

### Solution :

Method 1 (Binary Search) :
```python
class Solution:
    def minCost(self, nums: List[int], cost: List[int]) -> int:
        result = None
        minimum_equal_target = 1
        maximum_equal_target = 10**6
        while minimum_equal_target <= maximum_equal_target:
            middle = minimum_equal_target + (maximum_equal_target - minimum_equal_target) // 2
            temp_floor = 0
            temp_ceil = 0
            for index, num in enumerate(nums):
                temp_floor += abs(middle-num) * cost[index]
                temp_ceil += abs((middle+1)-num) * cost[index]
            
            result = min(temp_floor, temp_ceil) if result is None else min(result, temp_floor, temp_ceil)

            if temp_floor < temp_ceil:
                maximum_equal_target = middle - 1
            else:
                minimum_equal_target = middle + 1
        return result
```

### Nice Intuitions:

- [Weighted Median](https://leetcode.com/problems/minimum-cost-to-make-array-equal/solutions/2734183/python3-weighted-median-o-nlogn-with-explanations)
