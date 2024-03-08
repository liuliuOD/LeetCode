![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2962. [Count Subarrays Where Max Element Appears At Least K Times](https://leetcode.com/problems/count-subarrays-where-max-element-appears-at-least-k-times)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn count_subarrays(nums: Vec<i32>, k: i32) -> i64 {
        let n: usize = nums.len();
        let maximum: i32 = *nums.iter().max().unwrap();
        let mut left: usize = 0;
        let mut amount: i32 = 0;
        let mut result: i64 = 0;
        for right in 0..n {
            if nums[right] == maximum {
                amount += 1;
            }

            while amount >= k {
                result += (n - right) as i64;
                if nums[left] == maximum {
                    amount -= 1;
                }

                left += 1;
            }
        }

        return result
    }
}
```

Method 2 :
```rust
impl Solution {
    pub fn count_subarrays(nums: Vec<i32>, k: i32) -> i64 {
        let n: usize = nums.len();
        let maximum: i32 = *nums.iter().max().unwrap();
        let mut mapping: Vec<usize> = vec![];
        for (index, &num) in nums.iter().enumerate() {
            if num == maximum {
                mapping.push(index);
            }
        }

        let mut left: usize = 0;
        let mut amount: i32 = 0;
        let mut result: i64 = 0;
        for right in 0..mapping.len() {
            amount += 1;

            while amount >= k {
                result += (mapping[left] as i64 + 1) * match right == mapping.len()-1 {
                    true => (n - mapping[right]) as i64,
                    _ => (mapping[right+1] - mapping[right]) as i64,
                };

                amount -= 1;
                left += 1;
            }
        }

        return result
    }
}
```

### Solution :

Method 1 (In weekly contest 375, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def countSubarrays(self, nums: List[int], k: int) -> int:
        n = len(nums)
        maximum = max(nums)
        positions = []
        for index in range(n):
            if nums[index] == maximum:
                positions.append(index)

        n_positions = len(positions)
        result = 0
        for index in range(n_positions-k+1):
            result += (positions[index]+1) * (positions[index+k]-positions[index+k-1] if index+k < n_positions else n-positions[-1])

        return result
```

Method 2 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def countSubarrays(self, nums: List[int], k: int) -> int:
        n = len(nums)
        maximum = max(nums)
        left = 0
        amount = 0
        result = 0
        for right, num in enumerate(nums):
            if num == maximum:
                amount += 1

            while amount >= k:
                result += n - right
                if nums[left] == maximum:
                    amount -= 1

                left += 1

        return result
```
