![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## [Next Greater Element I](https://leetcode.com/problems/next-greater-element-i)

### Solution :

Method 1 (Monotonic Stack) :
```rust
use std::collections::HashMap;
impl Solution {
    pub fn next_greater_element(nums1: Vec<i32>, nums2: Vec<i32>) -> Vec<i32> {
        let mut stack = vec![];
        let mut next_greater_elements = HashMap::new();
        for index in (0..nums2.len()).rev() {
            while !stack.is_empty() {
                if let Some(item) = stack.pop() {
                    if item > nums2[index] {
                        next_greater_elements.insert(nums2[index], item);
                        stack.push(item);
                        break;
                    }
                }
            }
            if stack.is_empty() {
                next_greater_elements.insert(nums2[index], -1);
            }

            stack.push(nums2[index]);
        }

        let mut result = vec![];
        for item in nums1.iter() {
            result.push(next_greater_elements[item]);
        }
        result
    }
}
```

Method 2 (Monotonic Stack) :
```rust
use std::collections::HashMap;
impl Solution {
    pub fn next_greater_element(nums1: Vec<i32>, nums2: Vec<i32>) -> Vec<i32> {
        let mut stack = vec![];
        let mut next_greater_elements = HashMap::new();
        for index in (0..nums2.len()).rev() {
            while !stack.is_empty() {
                if let Some(&item) = stack.last() {
                    if item > nums2[index] {
                        next_greater_elements.insert(nums2[index], item);
                        break;
                    }

                    stack.pop();
                }
            }

            stack.push(nums2[index]);
        }
        
        nums1.into_iter().map(|item| next_greater_elements.get(&item).unwrap_or(&-1)).copied().collect()
    }
}
```
