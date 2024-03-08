![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1578. [Minimum Time To Make Rope Colorful](https://leetcode.com/problems/minimum-time-to-make-rope-colorful)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn min_cost(colors: String, needed_time: Vec<i32>) -> i32 {
        let n: usize = colors.len();
        /* Option 1 */
        let colors: &[u8] = colors.as_bytes();
        /* Option 2

        let colors: Vec<u8> = colors.bytes().collect();
        */
        let mut result: i32 = 0;
        let mut left: usize = 0;
        let mut right: usize = 0;
        while left < n {
            while right < n && colors[left] == colors[right] {
                right += 1;
            }

            result += needed_time[left..right].iter().sum::<i32>() - needed_time[left..right].iter().max().unwrap();
            left = right;
        }

        return result
    }
}
```

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N)$ (N: length of `colors`), Space Complexity: $O(1)$) :
```python
class Solution:
    def minCost(self, colors: str, needed_time: List[int]) -> int:
        n = len(colors)
        result = 0
        left = right = 0
        while left < n:
            while right < n and colors[right] == colors[left]:
                right += 1

            result += sum(needed_time[left:right]) - max(needed_time[left:right])
            left = right

        return result
```
