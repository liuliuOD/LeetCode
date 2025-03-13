![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3356. [Zero Array Transformation II](https://leetcode.com/problems/zero-array-transformation-ii)

### Solution :

Method 1 (AI by Grok3, Binary Search, ERROR: "Time Limit Exceeded", 622/627, Time Complexity: $O(M*N*Log(M))$, Space Complexity: $O(N)$ (M: the number of elements in `queries`, N: the number of elements in `nums`)) :
```rust
impl Solution {
    pub fn min_zero_array(nums: Vec<i32>, queries: Vec<Vec<i32>>) -> i32 {
        let n = nums.len();
        let m = queries.len();

        // Binary search over the number of queries
        let mut left = 0;
        let mut right = m as i32 + 1;

        while left < right {
            let mid = left + (right - left) / 2;

            // Check if we can make array zero with 'mid' queries
            if Self::can_make_zero(&nums, &queries, mid as usize) {
                right = mid; // Try fewer queries
            } else {
                left = mid + 1; // Need more queries
            }
        }

        return match left > m as i32 {
            true => -1, // Impossible
            _ => left // Minimum k found
        }
    }

    // Helper function to check if we can make array zero with k queries
    fn can_make_zero(nums: &Vec<i32>, queries: &Vec<Vec<i32>>, k: usize) -> bool {
        let n = nums.len();
        let mut delta: Vec<i64> = vec![0; n]; // Use i64 to avoid overflow

        // Apply first k queries
        for i in 0..k {
            let (l, r, val) = (queries[i][0] as usize, queries[i][1] as usize, queries[i][2] as i64);
            for j in l..=r {
                delta[j] += val; // Cumulative decrement possible at each index
            }
        }

        // Check if each element can be reduced to 0 or below
        for i in 0..n {
            if nums[i] as i64 > delta[i] {
                return false; // Can't reduce this element to 0
            }
        }

        return true
    }
}
```

Method 2 (AI by Grok3, Binary Search + Optimization, Time Complexity: $O((M+N)*Log(M))$, Space Complexity: $O(N)$ (M: the number of elements in `queries`, N: the number of elements in `nums`)) :
```rust
impl Solution {
    pub fn min_zero_array(nums: Vec<i32>, queries: Vec<Vec<i32>>) -> i32 {
        let m = queries.len();
        let n = nums.len();

        let mut left = 0;
        let mut right = m as i32 + 1;

        while left < right {
            let mid = left + (right - left) / 2;
            if Self::can_make_zero(&nums, &queries, mid as usize) {
                right = mid;
            } else {
                left = mid + 1;
            }
        }

        return match left > m as i32 {
            true => -1,
            _ => left
        }
    }

    fn can_make_zero(nums: &Vec<i32>, queries: &Vec<Vec<i32>>, k: usize) -> bool {
        let n = nums.len();
        let mut delta = vec![0i64; n + 1]; // Difference array

        // Build difference array for first k queries
        for i in 0..k {
            let (l, r, val) = (queries[i][0] as usize, queries[i][1] as usize, queries[i][2] as i64);
            delta[l] += val;
            if r + 1 < n {
                delta[r + 1] -= val;
            }
        }

        // Compute running sum and check
        let mut curr = 0i64;
        for i in 0..n {
            curr += delta[i];
            if nums[i] as i64 > curr {
                return false;
            }
        }

        return true
    }
}
```
