![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 673. [Number Of Longest Increasing Subsequence](https://leetcode.com/problems/number-of-longest-increasing-subsequence)

### Solution :

Method 1 (Dynamic Programming) :
```rust
use std::cmp::max;
impl Solution {
    pub fn find_number_of_lis(nums: Vec<i32>) -> i32 {
        let n: usize = nums.len();
        let mut memoization: Vec<i32> = vec![1; n];
        let mut times: Vec<i32> = vec![1; n];
        let mut maximum: i32 = 0;
        for index in 0..n {
            for index_previous in 0..index {
                if nums[index] <= nums[index_previous] {
                    continue;
                }

                if memoization[index_previous] >= memoization[index] {
                    memoization[index] = memoization[index_previous] + 1;
                    times[index] = times[index_previous];
                } else if memoization[index_previous]+1 == memoization[index] {
                    times[index] += times[index_previous];
                }
            }
            maximum = max(maximum, memoization[index]);
        }

        let mut result: i32 = 0;
        for index in 0..n {
            if memoization[index] == maximum {
                result += times[index];
            }
        }

        return result
    }
}
```

### Solution :

Method 1 (Dynamic Programming, ERROR: "Time Limit Exceeded", 93/223) :
```python
class Solution:
    def findNumberOfLIS(self, nums: List[int]) -> int:
        n = len(nums)
        maximum = 0
        memoization: List[Dict[int, int]] = [defaultdict(int) for _ in range(n)]
        for index in range(n):
            memoization[index][1] += 1
            for index_previous in range(index):
                if nums[index_previous] >= nums[index]:
                    continue

                for length, times in memoization[index_previous].items():
                    # previous length + current number = length + 1
                    memoization[index][length+1] += times
            maximum = max(maximum, max(memoization[index].keys()))

        result = 0
        for item in memoization:
            temp = Counter(item)
            if maximum in temp:
                result += temp[maximum]
        
        return result
```

Method 2 (Dynamic Programming) :
```python
class Solution:
    def findNumberOfLIS(self, nums: List[int]) -> int:
        n = len(nums)
        memoization = [1] * n
        times = [1] * n

        for index in range(n):
            for index_previous in range(index):
                if nums[index] > nums[index_previous]:
                    # find a longer subsequence
                    if memoization[index_previous] >= memoization[index]:
                        # record current length as LIS
                        memoization[index] = memoization[index_previous] + 1
                        # set LIS times to new LIS length times
                        times[index] = times[index_previous]
                    # find another subsequence with the same length to current LIS
                    elif memoization[index_previous]+1 == memoization[index]:
                        # add another LIS times
                        times[index] += times[index_previous]

        maximum = max(memoization)
        return sum([times[index] for index in range(n) if memoization[index] == maximum])
```
