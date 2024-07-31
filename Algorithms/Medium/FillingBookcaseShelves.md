![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1105. [Filling Bookcase Shelves](https://leetcode.com/problems/filling-bookcase-shelves)

### Solution :

Method 1 (DFS, Time Complexity: $(M*N)$, Space Complexity: $O(M*N)$ (M: numbers of the elements in `books`, N: value of `shelf_width`)) :
```rust
use std::cmp::Ordering;

impl Solution {
    pub fn min_height_shelves(books: Vec<Vec<i32>>, shelf_width: i32) -> i32 {
        let n: usize = books.len();
        let mut memoization: Vec<Vec<i32>> = Vec::with_capacity(n);
        for _ in 0..n {
            let mut item: Vec<i32> = Vec::with_capacity(shelf_width as usize);
            for _ in 0..=shelf_width {
                item.push(0);
            }
            memoization.push(item);
        }

        return Self::dfs(0, 0, 0, &mut memoization, &books, shelf_width)
    }

    fn dfs(index: usize, sum_width: i32, maximum_height: i32, memoization: &mut Vec<Vec<i32>>, books: &Vec<Vec<i32>>, shelf_width: i32) -> i32 {
        let n: usize = books.len();
        return match books[index].as_slice() {
            &[width, height] => {
                if index == n-1 {
                    return match (sum_width+width).cmp(&shelf_width) {
                        Ordering::Greater => maximum_height + height,
                        _ => maximum_height.max(height),
                    }
                }

                if memoization[index][sum_width as usize] != 0 {
                    return memoization[index][sum_width as usize]
                }

                memoization[index][sum_width as usize] = maximum_height + Self::dfs(index+1, width, height, memoization, books, shelf_width);
                if sum_width+width <= shelf_width {
                    memoization[index][sum_width as usize] = memoization[index][sum_width as usize].min(Self::dfs(index+1, sum_width+width, maximum_height.max(height), memoization, books, shelf_width));
                }

                return memoization[index][sum_width as usize]
            },
            _ => 0,
        }
    }
}
```
