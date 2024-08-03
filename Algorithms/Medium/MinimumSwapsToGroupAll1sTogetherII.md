![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2134. [Minimum Swaps To Group All 1's Together II](https://leetcode.com/problems/minimum-swaps-to-group-all-1s-together-ii)

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(M+N)$, Space Complexity: $O(1)$) :
```rust
impl Solution {
    pub fn min_swaps(nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let window: usize = nums.iter().filter(|&value| *value == 1).count();
        let mut result: i32 = i32::MAX;
        let mut index_left: usize = 0;
        let mut amount_zeros: i32 = 0;
        for index_right in 0..n+window {
            if nums[index_right%n] == 0 {
                amount_zeros += 1;
            }

            if index_right >= window-1 || window == 0 {
                if index_right >= window {
                    if nums[index_left%n] == 0 {
                        amount_zeros -= 1;
                    }

                    index_left += 1;
                }

                if result > amount_zeros {
                    result = amount_zeros;
                }
            }
        }

        return result
    }
}
```

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minSwaps(self, nums: List[int]) -> int:
        window = nums.count(1)
        nums *= 2
        result = inf
        amount_ones = 0
        amount_zeros = 0
        index_left = 0
        for index_right in range(len(nums)):
            if nums[index_right] == 0:
                amount_zeros += 1
            else:
                amount_ones += 1

            if index_right >= window:
                if nums[index_left] == 0:
                    amount_zeros -= 1
                else:
                    amount_ones -= 1

                index_left += 1

            if index_right >= window-1:
                result = min(result, amount_zeros)

        return result
```

Method 2 (Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minSwaps(self, nums: List[int]) -> int:
        window = nums.count(1)
        nums *= 2
        result = inf
        amount = [0, 0]
        index_left = 0
        for index_right in range(len(nums)):
            amount[nums[index_right]] += 1

            # Option 1
            if index_right >= window:
                amount[nums[index_left]] -= 1

                index_left += 1

            if index_right >= window-1:
                result = min(result, amount[0])
            """
            # Option 2

            if index_right >= window-1:
                if index_right >= window:
                    amount[nums[index_left]] -= 1

                    index_left += 1

                result = min(result, amount[0])
            """

        return result
```

Method 3 (Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(M)$ (M: number of `1` in `nums`, N: number of the elements in `nums`)) :
```python
class Solution:
    def minSwaps(self, nums: List[int]) -> int:
        window = nums.count(1)
        nums += nums[:window]
        result = inf
        amount_ones = 0
        index_left = 0
        for index_right in range(len(nums)):
            if nums[index_right] == 1:
                amount_ones += 1

            if index_right >= window-1:
                if index_right >= window:
                    # Option 1
                    if nums[index_left] == 1:
                        amount_ones -= 1
                    """
                    # Option 2

                    amount_ones -= int(nums[index_left] == 1)
                    """

                    index_left += 1

                result = min(result, window - amount_ones)

        return result
```

Method 4 (Two Pointer, Time Complexity: $O(M+N)$, Space Complexity: $O(1)$ (M: number of `1` in `nums`, N: number of the elements in `nums`)) :
```python
class Solution:
    def minSwaps(self, nums: List[int]) -> int:
        n = len(nums)
        window = nums.count(1)
        result = inf
        amount_ones = 0
        index_left = 0
        for index_right in range(n+window):
            if nums[index_right%n] == 1:
                amount_ones += 1

            if index_right >= window-1:
                if index_right >= window:
                    amount_ones -= int(nums[index_left%n] == 1)

                    index_left += 1

                result = min(result, window - amount_ones)

        return result
```
