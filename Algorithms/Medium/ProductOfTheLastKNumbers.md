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

Method 2 (Prefix Sum, Time Complexity: $O(M*K)$, Space Complexity: $O(M)$ (M: the number of invoking `add()`, K: the value that passed to `get_product()`)) :
```rust
struct ProductOfNumbers {
    prefix_sum: Vec<i32>,
}


/**
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
impl ProductOfNumbers {

    fn new() -> Self {
        return Self{
            prefix_sum: Vec::from([1]),
        }
    }

    fn add(&mut self, num: i32) {
        for index in 0..self.prefix_sum.len() {
            self.prefix_sum[index] *= num;
        }

        self.prefix_sum.push(num);
    }

    fn get_product(&self, k: i32) -> i32 {
        let n: usize = self.prefix_sum.len();

        return self.prefix_sum[n-k as usize]
    }
}
```

Method 3 (Prefix Sum + Optimization, Time Complexity: $O(M)$, Space Complexity: $O(M)$ (M: the number of invoking `add()`)) :
```rust
struct ProductOfNumbers {
    prefix_sum: Vec<i32>,
    size: usize,
}


/**
 * `&self` means the method takes an immutable reference.
 * If you need a mutable reference, change it to `&mut self` instead.
 */
impl ProductOfNumbers {

    fn new() -> Self {
        return Self{
            prefix_sum: Vec::from([1]),
            size: 0,
        }
    }

    fn add(&mut self, num: i32) {
        if num == 0 {
            self.prefix_sum = Vec::from([1]);
            self.size = 0;
            return
        }

        self.prefix_sum.push(*self.prefix_sum.last().unwrap() * num);
        self.size += 1;
    }

    fn get_product(&self, k: i32) -> i32 {
        let n: usize = self.prefix_sum.len();
        if n <= k as usize {
            return 0
        }

        return self.prefix_sum[n-1] / self.prefix_sum[n-k as usize - 1]
    }
}
```
