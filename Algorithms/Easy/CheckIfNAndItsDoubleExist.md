![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
![language-JAVA](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk)
---

## 1346. [Check If N And Its Double Exist](https://leetcode.com/problems/check-if-n-and-its-double-exist)

### Solution :

Method 1 (Hash Set, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: number of the elements in `arr`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn check_if_exist(arr: Vec<i32>) -> bool {
        let mut visited: HashSet<i32> = HashSet::new();
        for &num in arr.iter() {
            if num == 0 && visited.contains(&num) {
                return true
            }

            visited.insert(num);
        }

        return arr.iter()
            .filter(|&num| *num != 0 && visited.contains(&(*num * 2)))
            .collect::<Vec<&i32>>()
            .len() > 0
    }
}
```

Method 2 (BTree Hash Set, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: number of the elements in `arr`)) :
```rust
use std::collections::BTreeSet;

impl Solution {
    pub fn check_if_exist(arr: Vec<i32>) -> bool {
        let mut visited: BTreeSet<i32> = BTreeSet::new();
        for &num in arr.iter() {
            if num == 0 && visited.contains(&num) {
                return true
            }

            visited.insert(num);
        }

        return arr.iter()
            .filter(|&num| *num != 0 && visited.contains(&(*num * 2)))
            .collect::<Vec<&i32>>()
            .len() > 0
    }
}
```

Method 3 (Time Complexity: $O(N^2)$, Space Complexity: $O(N^2)$ (N: number of the elements in `arr`)) :
```rust
impl Solution {
    pub fn check_if_exist(arr: Vec<i32>) -> bool {
        let n: usize = arr.len();

        return (0..n)
            .flat_map(|index| (index+1..n).map(move |index_next| (index, index_next)))
            .filter(|&(i, j)| arr[i]<<1 == arr[j] || arr[j]<<1 == arr[i])
            .count() > 0
    }
}
```

### Solution :

Method 1 (Hash Set, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: number of the elements in `arr`)) :
```java
import java.util.HashSet;

class Solution {
    public boolean checkIfExist(int[] arr) {
        HashSet<Integer> set = new HashSet<>();
        for (int num: arr) {
            if (num == 0 && set.contains(num)) {
                return true;
            }

            set.add(num);
        }

        for (int num: arr) {
            if (num != 0 && set.contains(num*2)) {
                return true;
            }
        }

        return false;
    }
}
```

Method 2 (Hash Set, Time Complexity: $O(N)$, Space Complexity: $O(N)$ (N: number of the elements in `arr`)) :
```java
import java.util.HashSet;

class Solution {
    public boolean checkIfExist(int[] arr) {
        HashSet<Integer> set = new HashSet<>();

        for (int num: arr) {
            if (set.contains(num*2) || (num%2==0 && set.contains(num/2))) {
                return true;
            }

            set.add(num);
        }

        return false;
    }
}
```

Method 3 (Time Complexity: $O(N^2)$, Space Complexity: $O(N^2)$ (N: number of the elements in `arr`)) :
```java
class Solution {
    public boolean checkIfExist(int[] arr) {
        for (int index=0; index<arr.length; index++) {
            for (int index_next=index+1; index_next<arr.length; index_next++) {
                if (arr[index]<<1 == arr[index_next] || arr[index] == arr[index_next]<<1) {
                    return true;
                }
            }
        }

        return false;
    }
}
```
