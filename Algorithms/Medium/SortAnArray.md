![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 912. [Sort An Array](https://leetcode.com/problems/sort-an-array)

### Solution :

Method 1 (Counting Sort, Time Complexity: $(10^5)$, Space Complexity: $O(10^5)$) :
```rust
const AMOUNT: usize = 50_000;
const AMOUNT_LENGTH: usize = AMOUNT*2 + 1;
impl Solution {
    pub fn sort_array(nums: Vec<i32>) -> Vec<i32> {
        return Self::counting_sort(&nums)
    }

    fn counting_sort(nums: &Vec<i32>) -> Vec<i32> {
        let mut counter: [usize; AMOUNT_LENGTH] = [0; AMOUNT_LENGTH];
        for &num in nums {
            counter[num as usize +AMOUNT] += 1;
        }

        let mut prefix_sum: [usize; AMOUNT_LENGTH] = [0; AMOUNT_LENGTH];
        for index in 0..(AMOUNT_LENGTH) {
            prefix_sum[index] = counter[index];
            if index > 0 {
                prefix_sum[index] += prefix_sum[index-1];
            }
        }

        let n: usize = nums.len();
        let mut result: Vec<i32> = Vec::with_capacity(n);
        for _ in 0..n {
            result.push(0);
        }
        for &num in nums {
            prefix_sum[num as usize+AMOUNT] -= 1;
            result[prefix_sum[num as usize+AMOUNT]] = num;
        }

        return result
    }
}
```

Method 2 (Heap Sort, Time Complexity: $(N*Log(N))$, Space Complexity: $O(Log(N))$) :
```rust
impl Solution {
    pub fn sort_array(mut nums: Vec<i32>) -> Vec<i32> {
        Self::heap_sort(&mut nums);
        return nums
    }

    fn heap_sort(mut nums: &mut Vec<i32>) {
        let n: usize = nums.len();
        for index_root in (0..n/2).rev() {
            Self::heapify(index_root, nums, n);
        }

        for m in (1..n).rev() {
            nums.swap(0, m);
            Self::heapify(0, nums, m);
        }
    }

    fn heapify(index: usize, mut nums: &mut Vec<i32>, n: usize) {
        let mut index_root: usize = index;
        let index_left: usize = 2*index_root + 1;
        let index_right: usize = 2*index_root + 2;

        if index_left < n && nums[index_left] > nums[index_root] {
            index_root = index_left;
        }
        if index_right < n && nums[index_right] > nums[index_root] {
            index_root = index_right;
        }

        if index_root != index {
            nums.swap(index_root, index);
            Self::heapify(index_root, nums, n);
        }
    }
}
```

Method 3 (Heap Sort, Time Complexity: $(N*Log(N))$, Space Complexity: $O(Log(N))$) :
```rust
struct Heap<'a> {
    nums: &'a mut Vec<i32>,
}

impl<'a> Heap<'a> {

    fn new(nums: &'a mut Vec<i32>) -> Self {
        return Self {
            nums: nums,
        }
    }

    pub fn sort(&mut self) {
        let n: usize = self.nums.len();
        for index_root in (0..n/2).rev() {
            self.heapify(index_root, n);
        }

        for m in (1..n).rev() {
            self.nums.swap(0, m);
            self.heapify(0, m);
        }
    }

    fn heapify(&mut self, index: usize, n: usize) {
        let mut index_root: usize = index;
        let index_left: usize = 2*index_root + 1;
        let index_right: usize = 2*index_root + 2;

        if index_left < n && self.nums[index_left] > self.nums[index_root] {
            index_root = index_left;
        }
        if index_right < n && self.nums[index_right] > self.nums[index_root] {
            index_root = index_right;
        }

        if index_root != index {
            self.nums.swap(index_root, index);
            self.heapify(index_root, n);
        }
    }
}

impl Solution {
    pub fn sort_array(mut nums: Vec<i32>) -> Vec<i32> {
        Heap::new(&mut nums).sort();
        return nums
    }
}
```
