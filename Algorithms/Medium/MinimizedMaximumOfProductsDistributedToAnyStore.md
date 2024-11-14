![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2064. [Minimized Maximum Of Products Distributed To Any Store](https://leetcode.com/problems/minimized-maximum-of-products-distributed-to-any-store)

### Solution :

Method 1 (Binary Search, Time Complexity: $O(N*Log(M))$, Space Complexity: $O(1)$ (M: the maximum element in `quantities`, N: the number of the elements in `quantities`)) :
```rust
impl Solution {
    pub fn minimized_maximum(n: i32, quantities: Vec<i32>) -> i32 {
        let mut result: i32 = i32::MAX;
        let mut minimize: i32 = 1;
        let mut maximize: i32 = *quantities.iter().max().unwrap();
        while minimize <= maximize {
            let middle: i32 = minimize + (maximize-minimize)/2;

            let mut amount_stores: i32 = 0;
            for &quantity in quantities.iter() {
                amount_stores += (quantity+middle-1) / middle;
                if amount_stores > n {
                    break;
                }
            }

            if amount_stores > n {
                minimize = middle + 1;
            } else {
                if middle == 0 {
                    break;
                }
                maximize = middle - 1;
            }
        }

        return minimize
    }
}
```
