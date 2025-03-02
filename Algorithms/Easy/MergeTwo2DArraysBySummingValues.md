![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 2570. [Merge Two 2D Arrays By Summing Values](https://leetcode.com/problems/merge-two-2d-arrays-by-summing-values)

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(M+N)$, Space Complexity: $O(1)$ (M: the number of the elements in `nums1`, N: the number of the elements in `nums2`)) :
```rust
impl Solution {
    pub fn merge_arrays(nums1: Vec<Vec<i32>>, nums2: Vec<Vec<i32>>) -> Vec<Vec<i32>> {
        let m: usize = nums1.len();
        let n: usize = nums2.len();
        let mut result: Vec<Vec<i32>> = Vec::new();
        let mut index_m: usize = 0;
        let mut index_n: usize = 0;
        while index_m < m || index_n < n {
            if index_m < m && index_n < n {
                if nums1[index_m][0] < nums2[index_n][0] {
                    Self::merge(nums1[index_m].clone(), &mut result);
                    index_m += 1;
                } else if nums1[index_m][0] > nums2[index_n][0] {
                    Self::merge(nums2[index_n].clone(), &mut result);
                    index_n += 1;
                } else {
                    Self::merge(nums1[index_m].clone(), &mut result);
                    Self::merge(nums2[index_n].clone(), &mut result);
                    index_m += 1;
                    index_n += 1;
                }
            } else if index_m < m {
                Self::merge(nums1[index_m].clone(), &mut result);
                index_m += 1;
            } else if index_n < n {
                Self::merge(nums2[index_n].clone(), &mut result);
                index_n += 1;
            }
        }

        return result
    }

    fn merge(item: Vec<i32>, result: &mut Vec<Vec<i32>>) {
        let n: usize = result.len();
        if n == 0 {
            result.push(item);
            return
        }

        if result[n-1][0] == item[0] {
            result[n-1][1] += item[1];
            return
        }

        result.push(item);
    }
}
```
