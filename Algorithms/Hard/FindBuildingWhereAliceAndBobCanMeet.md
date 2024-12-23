![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2940. [Find Building Where Alice And Bob Can Meet](https://leetcode.com/problems/find-building-where-alice-and-bob-can-meet)

### Solution :

Method 1 (Monotonic decreasing stack, Time Complexity: $O(N*Log(M))$, Space Complexity: $O(M)$ (M: the number of the elements in `heights`, N: the number of the elements in `queries`)) :
```rust
impl Solution {
    pub fn leftmost_building_queries(heights: Vec<i32>, queries: Vec<Vec<i32>>) -> Vec<i32> {
        let m: usize = heights.len();
        let n: usize = queries.len();
        let mut queries_reformat: Vec<Vec<(i32, usize)>> = vec![vec![]; m];
        let mut result: Vec<i32> = vec![-1; n];
        for index_query in 0..n {
            let mut a: usize = queries[index_query][0] as usize;
            let mut b: usize = queries[index_query][1] as usize;
            if a > b {
                std::mem::swap(&mut a, &mut b);
            }

            if (heights[a] < heights[b]) || (a == b) {
                result[index_query] = b as i32;
                continue;
            }

            queries_reformat[b].push((heights[a], index_query));
        }

        let mut mono_stack: Vec<(i32, usize)> = Vec::new();
        for b in (0..m).rev() {
            for &(height_a, index_query) in &queries_reformat[b] {
                let index_stack: usize = Self::binary_search(height_a, &mono_stack);
                if index_stack < mono_stack.len() && mono_stack[index_stack].0 > height_a {
                    result[index_query] = mono_stack[index_stack].1 as i32;
                }
            }

            while mono_stack.len() > 0 && mono_stack.last().unwrap().0 <= heights[b] {
                mono_stack.pop();
            }
            mono_stack.push((heights[b], b));
        }

        return result
    }

    fn binary_search(target: i32, mono_stack: &Vec<(i32, usize)>) -> usize {
        let n: usize = mono_stack.len();
        let mut left = 0;
        let mut right = n - 1;
        while left <= right && right < n {
            let middle = left + (right-left)/2;
            if mono_stack[middle].0 > target {
                left = middle + 1;
            } else {
                right = middle - 1;
            }
        }

        return right
    }
}
```
