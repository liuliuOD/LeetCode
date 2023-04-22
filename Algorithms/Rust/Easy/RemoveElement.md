## [Remove Element](https://leetcode.com/problems/remove-element)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn remove_element(nums: &mut Vec<i32>, val: i32) -> i32 {
        nums.retain(|&item| item != val);

        nums.len() as _
    }
}
```

Method 2 (remove takes linear time, much more inefficient) :
```rust
impl Solution {
    pub fn remove_element(nums: &mut Vec<i32>, val: i32) -> i32 {
        let mut i = 0;
        while i < nums.len() {
            if nums[i] == val {
                nums.remove(i);
                continue;
            }
            i += 1;
        }

        nums.len() as _
    }
}
```

Method 3 :
```rust
impl Solution {
    pub fn remove_element(nums: &mut Vec<i32>, val: i32) -> i32 {
        let mut last_offset = 1;
        let mut i = 0;
        let length = nums.len();
        while i < length {
            if nums[i] == -1 {
                break;
            }

            match nums[i] == val {
                true => {
                    nums[i] = nums[length - last_offset];
                    nums[length - last_offset] = -1;
                    last_offset += 1;
                },
                false => i += 1,
            }
        }

        (length - last_offset + 1) as _
    }
}
```
