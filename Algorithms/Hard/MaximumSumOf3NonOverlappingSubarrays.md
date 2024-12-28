![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 689. [Maximum Sum Of 3 Non-Overlapping Subarrays](https://leetcode.com/problems/maximum-sum-of-3-non-overlapping-subarrays)

### Solution :

Method 1 (DFS + Memoization, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of the elements in `nums`)) :
```rust
impl Solution {
    pub fn max_sum_of_three_subarrays(nums: Vec<i32>, k: i32) -> Vec<i32> {
        let k: usize = k as usize;
        let n: usize = nums.len();
        let m: usize = n - k + 1;
        let mut sums: Vec<i32> = vec![0; m];
        let mut sum: i32 = 0;
        for index in 0..n {
            sum += nums[index];
            if index >= k {
                sum -= nums[index-k];
            }

            if index+1 >= k {
                sums[index-k+1] = sum;
            }
        }

        let mut memoization: Vec<Vec<i32>> = vec![vec![-1; 4]; m];
        Self::dfs(&mut memoization, 0, 3, k, &sums);

        let mut result: Vec<i32> = Vec::new();
        Self::find_maximum(&mut result, &mut memoization, 0, 3, k, &sums);
        return result
    }

    fn dfs(memoization: &mut Vec<Vec<i32>>, index: usize, amount_remaining: i32, k: usize, sums: &Vec<i32>) -> i32 {
        if amount_remaining == 0 {
            return 0
        }
        if index >= sums.len() {
            return i32::MIN
        }

        if memoization[index][amount_remaining as usize] != -1 {
            return memoization[index][amount_remaining as usize]
        }

        let choose: i32 = sums[index] + Self::dfs(memoization, index+k, amount_remaining-1, k, sums);
        let skip: i32 = Self::dfs(memoization, index+1, amount_remaining, k, sums);
        memoization[index][amount_remaining as usize] = i32::max(choose, skip);
        return memoization[index][amount_remaining as usize]
    }

    fn find_maximum(result: &mut Vec<i32>, memoization: &mut Vec<Vec<i32>>, index: usize, amount_remaining: i32, k: usize, sums: &Vec<i32>) {
        if amount_remaining == 0 || index >= sums.len() {
            return
        }

        let choose: i32 = sums[index] + Self::dfs(memoization, index+k, amount_remaining-1, k, sums);
        let skip: i32 = Self::dfs(memoization, index+1, amount_remaining, k, sums);
        if choose >= skip {
            result.push(index as i32);
            Self::find_maximum(result, memoization, index+k, amount_remaining-1, k, sums);
        } else {
            Self::find_maximum(result, memoization, index+1, amount_remaining, k, sums);
        }
    }
}
```
