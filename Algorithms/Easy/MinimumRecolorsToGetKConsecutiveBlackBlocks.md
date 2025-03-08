![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2379. [Minimum Recolors To Get K Consecutive Black Blocks](https://leetcode.com/problems/minimum-recolors-to-get-k-consecutive-black-blocks)

### Solution :

Method 1 (Backtracking, ERROR: "Time Limit Exceeded", 17/122, Time Complexity: $O(2^N)$, Space Complexity: $O(N)$ (N: the number of elements in `blocks`)) :
```rust
impl Solution {
    pub fn minimum_recolors(blocks: String, k: i32) -> i32 {
        let blocks: &[u8] = blocks.as_bytes();
        return Self::backtracking(0, 0, 0, blocks, k)
    }

    fn backtracking(index: usize, amount_operation: i32, amount_cumulative: i32, blocks: &[u8], k: i32) -> i32 {
        let n: usize = blocks.len();
        if amount_cumulative >= k {
            return amount_operation
        }

        if index >= n {
            return i32::MAX
        }

        let mut result: i32 = i32::MAX;
        if blocks[index] == b'B' {
            result = i32::min(result, Self::backtracking(index+1, amount_operation, amount_cumulative+1, blocks, k));
        } else {
            result = i32::min(result, i32::min(Self::backtracking(index+1, amount_operation+1, amount_cumulative+1, blocks, k), Self::backtracking(index+1, 0, 0, blocks, k)));
        }

        return result
    }
}
```

Method 2 (AI by Grok3, Sliding Window, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: the number of elements in `blocks`)) :
```rust
impl Solution {
    pub fn minimum_recolors(blocks: String, k: i32) -> i32 {
        let blocks: Vec<char> = blocks.chars().collect();
        let k = k as usize;
        let n = blocks.len();

        // Count white blocks in first window of size k
        let mut white_count = 0;
        for i in 0..k {
            if blocks[i] == 'W' {
                white_count += 1;
            }
        }

        // This will be our answer - minimum white blocks to recolor
        let mut min_recolors = white_count;

        // Slide window from k to end
        for i in k..n {
            // Remove leftmost block of previous window
            if blocks[i - k] == 'W' {
                white_count -= 1;
            }
            // Add rightmost block of current window
            if blocks[i] == 'W' {
                white_count += 1;
            }
            // Update minimum if current is smaller
            min_recolors = min_recolors.min(white_count);
        }

        min_recolors
    }
}
```
