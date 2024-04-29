![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2997. [Minimum Number Of Operations To Make Array XOR Equal To K](https://leetcode.com/problems/minimum-number-of-operations-to-make-array-xor-equal-to-k)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```rust
impl Solution {
    pub fn min_operations(nums: Vec<i32>, k: i32) -> i32 {
        let mut current: i32 = k;
        for num in nums {
            current ^= num;
        }

        /* Option 1 */
        let mut result: i32 = 0;
        while current > 0 {
            result += current % 2;
            current /= 2;
        }

        return result
        /* Option 2

        return current.count_ones() as i32
        */
    }
}
```

Method 2 (Built-In method, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```rust
impl Solution {
    pub fn min_operations(nums: Vec<i32>, k: i32) -> i32 {
        return nums.into_iter().fold(k, |a, b| a ^ b).count_ones() as i32
    }
}
```

### Solution :

Method 1 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minOperations(self, nums: List[int], k: int) -> int:
        bits_k = list(map(int, bin(k)[2:]))[::-1]
        bits_another = set()
        for num in nums:
            for index, bit_num in enumerate(reversed(bin(num)[2:])):
                bit_num = int(bit_num)
                if index >= len(bits_k):
                    key = (index, bit_num)
                    if key in bits_another:
                        bits_another.remove(key)
                    else:
                        bits_another.add(key)

                    continue

                bits_k[index] = bits_k[index] ^ bit_num

        result = bits_k.count(1)
        while bits_another:
            result += bits_another.pop()[1]
        return result
```

Method 2 (Brute Force, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minOperations(self, nums: List[int], k: int) -> int:
        current = [0] * 20
        # Option 1
        for num in nums:
            index = 0
            while num:
                bit = num % 2
                num //= 2
                current[index] ^= bit
                index += 1

        index = 0
        while k:
            bit = k % 2
            k //= 2
            current[index] ^= bit
            index += 1
        """
        # Option 2

        nums.append(k)
        for num in nums:
            index = 0
            while num:
                bit = num % 2
                num //= 2
                current[index] ^= bit
                index += 1
        """
        return sum(current)
```

Method 3 (Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minOperations(self, nums: List[int], k: int) -> int:
        current = 0
        nums.append(k)
        for num in nums:
            current ^= num

        # Option 1
        return bin(current).count("1")
        """
        # Option 2

        return current.bit_count()
        """
```
