![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 733. [Flood Fill](https://leetcode.com/problems/flood-fill)

### Solution :

Method 1 (Hash Set + Stack, Time Complexity: $O(M*N)$, Space Complexity: $O(M*N)$) :
```rust
use std::collections::HashSet;
impl Solution {
    pub fn flood_fill(mut image: Vec<Vec<i32>>, sr: i32, sc: i32, color: i32) -> Vec<Vec<i32>> {
        let sr: usize = sr as usize;
        let sc: usize = sc as usize;
        let color_origin: i32 = image[sr][sc];
        let m: usize = image.len();
        let n: usize = image[0].len();
        let mut visited: HashSet<(usize, usize)> = HashSet::new();
        let mut stack: Vec<(usize, usize)> = vec![(sr, sc)];
        while stack.len() > 0 {
            let (index_m, index_n) = stack.pop().unwrap();
            if index_m >= m || index_n >= n {
                continue;
            }

            let key: (usize, usize) = (index_m, index_n);
            if visited.contains(&key) {
                continue;
            }
            visited.insert(key);

            if image[index_m][index_n] != color_origin {
                continue;
            }
            image[index_m][index_n] = color;
            /* Option 1 */
            stack.push((index_m-1, index_n));
            stack.push((index_m+1, index_n));
            stack.push((index_m, index_n-1));
            stack.push((index_m, index_n+1));
            /* Option 2

            for (offset_m, offset_n) in [(-1, 0), (1, 0), (0, -1), (0, 1)] {
                stack.push((((index_m as i32)+offset_m) as usize, ((index_n as i32)+offset_n) as usize));
            }
            */
        }

        return image
    }
}
```
