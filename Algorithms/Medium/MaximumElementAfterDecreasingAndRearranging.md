![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1846. [Maximum Element After Decreasing And Rearranging](https://leetcode.com/problems/maximum-element-after-decreasing-and-rearranging)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn maximum_element_after_decrementing_and_rearranging(arr: Vec<i32>) -> i32 {
        let mut arr: Vec<i32> = arr;
        arr.sort();
        /* Option 1 */
        arr[0] = 1;
        for index in 1..arr.len() {
            if arr[index] == arr[index-1] {
                continue;
            }

            arr[index] = arr[index-1] + 1;
        }

        return arr[arr.len()-1]
        /* Option 2
        
        let mut result: i32 = 1;
        for index in 1..arr.len() {
            if arr[index] <= result {
                continue;
            }

            result += 1;
        }

        return result
        */
    }
}
```

Method 2 (Counting Sort) :
```rust
impl Solution {
    pub fn maximum_element_after_decrementing_and_rearranging(nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let mut counting: Vec<i32> = vec![0; n+1];
        for num in nums {
            counting[(num as usize).min(n)] += 1;
        }

        let mut result: i32 = 0;
        for (num, amount) in counting.iter_mut().enumerate() {
            let num: i32 = num as i32;
            while *amount > 0 && num > result {
                result += 1;
                *amount -= 1;
            }
        }

        return result
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def maximumElementAfterDecrementingAndRearranging(self, arr: List[int]) -> int:
        arr.sort()
        arr[0] = 1
        for index in range(1, len(arr)):
            if arr[index] > arr[index-1]:
                arr[index] = arr[index-1] + 1

        return arr[-1]
```

Method 2 (Counting Sort, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def maximumElementAfterDecrementingAndRearranging(self, nums: List[int]) -> int:
        n = len(nums)
        counting = [0] * (n+1)
        for num in nums:
            # because the maximum element in the list won't larger than the list length, so we can say that when `num > n` then we treat it as `n`.
            counting[min(num, n)] += 1

        result = 0
        for num, amount in enumerate(counting):
            while amount > 0 and num > result:
                result += 1
                amount -= 1

        return result
```
