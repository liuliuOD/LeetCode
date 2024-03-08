![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 2433. [Find The Original Array Of Prefix XOR](https://leetcode.com/problems/find-the-original-array-of-prefix-xor)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn find_array(pref: Vec<i32>) -> Vec<i32> {
        return vec![pref[0]].into_iter().chain((1..pref.len()).map(|index| pref[index-1]^pref[index]).collect::<Vec<i32>>()).collect()
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def findArray(self, pref: List[int]) -> List[int]:
        # Option 1
        result = [pref[0]]
        for index in range(1, len(pref)):
            result.append(pref[index-1] ^ pref[index])

        return result
        """
        # Option 2

        return [pref[0]] + [pref[index-1] ^ pref[index] for index in range(1, len(pref))]
        """
```

Method 2 (Time Complexity: $O(N)$, Space Complexity: $O(1)$) :
```python
class Solution:
    def findArray(self, pref: List[int]) -> List[int]:
        # use `temp` to record the XOr result that includes all the items before the index
        temp = pref[0]
        for index in range(1, len(pref)):
            """
            if A ^ B = C, then A ^ C = B and B ^ C = A
            """
            pref[index] = temp ^ pref[index]
            temp ^= pref[index]

        return pref
```
