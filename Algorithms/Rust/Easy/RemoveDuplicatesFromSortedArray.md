## [Remove Duplicates From Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn remove_duplicates(nums: &mut Vec<i32>) -> i32 {
        let mut previous = -101;
        let mut i = 0;
        while i < nums.len() {
            match nums[i] == previous {
                true => {
                    nums.remove(i);
                },
                false => {
                    previous = nums[i];
                    i += 1;
                },
            };
        }

        nums.len() as _
    }
}
```

Method 2 :
```rust
impl Solution {
    pub fn remove_duplicates(nums: &mut Vec<i32>) -> i32 {
        match nums.len() <= 1 {
            true => nums.len() as _,
            false => {
                let mut distinct_index = 0;
                for i in 1..nums.len() {
                    if nums[i] != nums[distinct_index] {
                        nums[distinct_index + 1] = nums[i];
                        distinct_index += 1;
                    }
                }
                
                (distinct_index + 1) as _
            }
        }
    }
}
```

Method 3 (standard library) :
```rust
impl Solution {
    pub fn remove_duplicates(nums: &mut Vec<i32>) -> i32 {
        nums.dedup();

        nums.len() as _
    }
}
```
