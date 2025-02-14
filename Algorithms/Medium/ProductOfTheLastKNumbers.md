![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1352. [Product Of The Last K Numbers](https://leetcode.com/problems/product-of-the-last-k-numbers)

### Solution :

```rust
/**
 * Your ProductOfNumbers object will be instantiated and called as such:
 * let obj = ProductOfNumbers::new();
 * obj.add(num);
 * let ret_2: i32 = obj.get_product(k);
 */
```

Method 1 (Brute Force, Time Complexity: $O(M*K)$, Space Complexity: $O(M)$ (M: the number of invoking `add()`, K: the value that passed to `get_product()`)) :
```rust
struct ProductOfNumbers {
    nums: Vec<i32>,
}


/** 
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
impl ProductOfNumbers {

    fn new() -> Self {
        return Self{
            nums: Vec::new(),
        }
    }

    fn add(&mut self, num: i32) {
        self.nums.push(num);
    }

    fn get_product(&self, k: i32) -> i32 {
        let mut result: i32 = 1;
        let n: usize = self.nums.len();
        for index in (n-k as usize)..n {
            result *= self.nums[index];
        }

        return result
    }
}
```
