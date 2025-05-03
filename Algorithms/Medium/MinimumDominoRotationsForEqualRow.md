![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1007. [Minimum Domino Rotations For Equal Row](https://leetcode.com/problems/minimum-domino-rotations-for-equal-row)

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(1)$ (N: the number of the elements in `tops`)) :
```rust
impl Solution {
    pub fn min_domino_rotations(tops: Vec<i32>, bottoms: Vec<i32>) -> i32 {
        let n: usize = tops.len();
        let result_top: i32 = i32::min(Self::traverse(0, tops[0], &tops, &bottoms), Self::traverse(1, bottoms[0], &tops, &bottoms));
        let result_bottom: i32 = i32::min(Self::traverse(0, bottoms[0], &bottoms, &tops), Self::traverse(1, tops[0], &bottoms, &tops));

        return if result_top == i32::MAX && result_bottom == i32::MAX {
            -1
        } else if result_top == i32::MAX {
            result_bottom
        } else if result_bottom == i32::MAX {
            result_top
        } else {
            i32::min(result_top, result_bottom)
        }
    }

    fn traverse(mut result: i32, target: i32, candidates_a: &Vec<i32>, candidates_b: &Vec<i32>) -> i32 {
        let n: usize = candidates_a.len();
        for index in 1..n {
            if candidates_a[index] == target {
                continue;
            } else if candidates_b[index] == target {
                result += 1;
                continue;
            }

            return i32::MAX
        }

        return result
    }
}
```
