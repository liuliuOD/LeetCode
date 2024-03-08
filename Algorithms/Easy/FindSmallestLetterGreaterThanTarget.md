![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 744. [Find Smallest Letter Greater Than Target](https://leetcode.com/problems/find-smallest-letter-greater-than-target)

### Solution :

Method 1 (Time Complexity: $O(N)$) :
```rust
impl Solution {
    pub fn next_greatest_letter(letters: Vec<char>, target: char) -> char {
        let mut result: char = letters[0];
        for ch in letters.into_iter() {
            if ch > target {
                result = ch;
                break;
            }
        }
        return result
    }
}
```

### Solution :

Method 1 (Time Complexity: $O(N)$) :
```python
class Solution:
    def nextGreatestLetter(self, letters: List[str], target: str) -> str:
        result = letters[0]
        for char in letters:
            if char > target:
                result = char
                break
        return result
```

Method 2 (Binary Search, use Right) :
```python
class Solution:
    def nextGreatestLetter(self, letters: List[str], target: str) -> str:
        left = -1
        right = len(letters) - 1
        while left+1 < right:
            middle = (left + right) // 2
            if letters[middle] <= target:
                left = middle
            else:
                right = middle
        return letters[right] if letters[right] > target else letters[0]
```

Method 3 (Binary Search, use Left) :
```python
class Solution:
    def nextGreatestLetter(self, letters: List[str], target: str) -> str:
        left = 0
        right = len(letters) - 1
        while left <= right:
            middle = (left + right) // 2
            if letters[middle] <= target:
                left = middle + 1
            else:
                right = middle - 1
        return letters[left] if left < len(letters) else letters[0]
```
