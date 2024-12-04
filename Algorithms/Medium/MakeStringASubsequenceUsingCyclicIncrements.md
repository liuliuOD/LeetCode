![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-PHP](https://img.shields.io/badge/PHP-acb1f9?style=for-the-badge&logo=PHP)
![language-JAVA](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk)
---

## 2825. [Make String A Subsequence Using Cyclic Increments](https://leetcode.com/problems/make-string-a-subsequence-using-cyclic-increments)

### Solution :

Method 1 (Two Pointers, Time Complexity: $O(M)$, Space Complexity: $O(M+N)$ (M: the length of `str1`, N: the length of `str2`)) :
```rust
impl Solution {
    pub fn can_make_subsequence(str1: String, str2: String) -> bool {
        let mut index1: usize = 0;
        let mut index2: usize = 0;
        let str1_char: Vec<char> = str1.chars().collect::<Vec<char>>();
        let str2_char: Vec<char> = str2.chars().collect::<Vec<char>>();
        while index1 < str1.len() {
            if str1_char[index1] == str2_char[index2] || (str1_char[index1] == 'z' && str2_char[index2] == 'a') || (str1_char[index1] as u8 - b'a' + 1 == str2_char[index2] as u8 - b'a') {
                index2 += 1;
            }

            if index2 >= str2.len() {
                return true
            }

            index1 += 1;
        }

        return false
    }
}
```

Method 2 (Two Pointers, Time Complexity: $O(M)$, Space Complexity: $O(M+N)$ (M: the length of `str1`, N: the length of `str2`)) :
```rust
const BASE: u8 = b'a';

impl Solution {
    pub fn can_make_subsequence(str1: String, str2: String) -> bool {
        let m: usize = str1.len();
        let n: usize = str2.len();
        if m < n {
            return false
        }

        let mut index1: usize = 0;
        let mut index2: usize = 0;
        let str1_char: Vec<char> = str1.chars().collect::<Vec<char>>();
        let str2_char: Vec<char> = str2.chars().collect::<Vec<char>>();
        while index1 < m {
            if str1_char[index1] == str2_char[index2] || (str1_char[index1] == 'z' && str2_char[index2] == 'a') || (str1_char[index1] as u8-BASE+1 == str2_char[index2] as u8-BASE) {
                index2 += 1;
            }

            if index2 >= n {
                return true
            }

            index1 += 1;
        }

        return false
    }
}
```

Method 3 (Two Pointers, Time Complexity: $O(M)$, Space Complexity: $O(M+N)$ (M: the length of `str1`, N: the length of `str2`)) :
```rust
impl Solution {
    pub fn can_make_subsequence(str1: String, str2: String) -> bool {
        let m: usize = str1.len();
        let n: usize = str2.len();
        if m < n {
            return false
        }

        let mut index1: usize = 0;
        let mut index2: usize = 0;
        let str1_char: Vec<char> = str1.chars().collect::<Vec<char>>();
        let str2_char: Vec<char> = str2.chars().collect::<Vec<char>>();
        while index1 < m {
            let ascii1: u8 = str1_char[index1] as u8;
            let ascii2: u8 = str2_char[index2] as u8;
            if ascii1 == ascii2 || (ascii1-ascii2 == 25) || (ascii1+1 == ascii2) {
                index2 += 1;
            }

            if index2 >= n {
                return true
            }

            index1 += 1;
        }

        return false
    }
}
```

### Solution :

Method 1 (Two Pointers) :
```python
class Solution:
    def canMakeSubsequence(self, str1: str, str2: str) -> bool:
        len_1 = len(str1)
        len_2 = len(str2)
        if len_2 > len_1:
            return False

        pointer_1 = pointer_2 = 0
        while pointer_1 < len_1 and pointer_2 < len_2:
            if str1[pointer_1] == str2[pointer_2]:
                pointer_1 += 1
                pointer_2 += 1
                continue

            char = chr(ord(str1[pointer_1])+1) if ord(str1[pointer_1])+1 <= ord('z') else 'a'
            if char == str2[pointer_2]:
                pointer_2 += 1

            pointer_1 += 1
        return pointer_2 >= len_2
```

Method 2 (Two Pointers) :
```python
class Solution:
    def canMakeSubsequence(self, str1: str, str2: str) -> bool:
        len_1 = len(str1)
        len_2 = len(str2)
        if len_2 > len_1:
            return False

        pointer_1 = pointer_2 = 0
        while pointer_1 < len_1 and pointer_2 < len_2:
            if (str1[pointer_1] == str2[pointer_2]) or (ord(str1[pointer_1])-ord(str2[pointer_2]) == -1) or (str1[pointer_1] == 'z' and str2[pointer_2] == 'a'):
                pointer_2 += 1

            pointer_1 += 1

        return pointer_2 >= len_2
```

### Solution :

Method 1 (Two Pointers) :
```php
class Solution {

    /**
     * @param String $str1
     * @param String $str2
     * @return Boolean
     */
    function canMakeSubsequence($str1, $str2) {
        $len1 = strlen($str1);
        $len2 = strlen($str2);
        if ($len2 > $len1) {
            return false;
        }

        $pointer1 = $pointer2 = 0;
        while ($pointer1 < $len1 && $pointer2 < $len2) {
            $char1 = $str1[$pointer1];
            $char2 = $str2[$pointer2];
            $pointer1++;
            if (
                ($char1 === $char2)
                || ($char1 === 'z' && $char2 === 'a')
                || (++$char1 === $char2) // $char1 has been modified
            ) {
                $pointer2++;
            }
        }

        return $pointer2 >= $len2;
    }
}
```

### Solution :

Method 1 (Two Pointers, Time Complexity: $O(M)$, Space Complexity: $O(M+N)$ (M: the length of `str1`, N: the length of `str2`)) :
```java
class Solution {
    public boolean canMakeSubsequence(String str1, String str2) {
        int m = str1.length();
        int n = str2.length();
        if (m < n) {
            return false;
        }

        int index1 = 0;
        int index2 = 0;
        while (index1 < m) {
            if ((str1.charAt(index1) == str2.charAt(index2)) || (str2.charAt(index2)-str1.charAt(index1)==1) || (str1.charAt(index1)-str2.charAt(index2)==25)) {
                index2++;
            }

            if (index2 >= n) {
                return true;
            }

            index1++;
        }

        return false;
    }
}
```
