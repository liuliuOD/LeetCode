![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 3394. [Check If Grid Can Be Cut Into Sections](https://leetcode.com/problems/check-if-grid-can-be-cut-into-sections)

### Solution :

Method 1 (Sort, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$ (N: the number of elements in `rectangles`)) :
```rust
impl Solution {
    pub fn check_valid_cuts(n: i32, rectangles: Vec<Vec<i32>>) -> bool {
        let mut x_axis: Vec<(i32, i32)> = Vec::new();
        let mut y_axis: Vec<(i32, i32)> = Vec::new();
        for rectangle in rectangles {
            x_axis.push((rectangle[0], rectangle[2]));
            y_axis.push((rectangle[1], rectangle[3]));
        }

        if Self::can_cut(x_axis) {
            return true
        }
        if Self::can_cut(y_axis) {
            return true
        }

        return false
    }

    fn can_cut(mut elements: Vec<(i32, i32)>) -> bool {
        elements.sort();

        let n: usize = elements.len();
        let mut amount: i32 = 1;
        let mut maximum: i32 = elements[0].1;
        for index in 1..n {
            if maximum <= elements[index].0 {
                amount += 1;
            }
            maximum = i32::max(maximum, elements[index].1);
        }

        return amount >= 3
    }
}
```
