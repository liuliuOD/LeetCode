![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2090. [K Radius Subarray Averages](https://leetcode.com/problems/k-radius-subarray-averages)

### Solution :

Method 1 (Sliding Window) :
```rust
impl Solution {
    pub fn get_averages(nums: Vec<i32>, k: i32) -> Vec<i32> {
        let k = k as usize;
        let n: usize = nums.len();
        let mut result: Vec<i32> = vec![-1; n];

        let mut temp: i64 = 0;
        for index in 0..n {
            temp += nums[index] as i64;

            if index < k*2 {
                continue;
            }

            if index > k*2 {
                temp -= nums[index-k*2-1] as i64;
            }

            result[index-k] = (temp / (k*2+1) as i64) as i32;
        }
        return result
    }
}
```

### Solution :

Method 1 (Sliding Window) :
```python
class Solution:
    def getAverages(self, nums: List[int], k: int) -> List[int]:
        result = [-1 for _ in range(len(nums))]

        temp = 0
        for index in range(len(nums)):
            temp += nums[index]
            if index < k*2:
                continue

            if index > k*2:
                temp -= nums[index-k*2-1]
            
            result[index-k] = temp // (k*2+1)

        return result
```
