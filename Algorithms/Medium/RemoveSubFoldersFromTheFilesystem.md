![language-RUST](https://img.shields.io/badge/RUST-8d4004?style=for-the-badge&logo=RUST)
---

## 1233. [Remove Sub-Folders From The Filesystem](https://leetcode.com/problems/remove-sub-folders-from-the-filesystem)

### Solution :

Method 1 (Brute Force, ERROR: "Time Limit Exceeded", 28/34, Time Complexity: $O(N^2)$, Space Complexity: $O(N)$ (N: the number of the elements in `folder`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn remove_subfolders(mut folder: Vec<String>) -> Vec<String> {
        let n: usize = folder.len();
        folder.sort();
        let mut visited: HashSet<usize> = HashSet::new();
        let mut result: Vec<String> = Vec::new();
        for index_start in 0..n {
            if visited.contains(&index_start) {
                continue;
            }

            for index in 0..n {
                if index_start == index {
                    continue;
                }

                if folder[index].starts_with(&(folder[index_start].clone()+"/")) {
                    visited.insert(index);
                }
            }

            result.push(folder[index_start].clone());
        }

        return result
    }
}
```

Method 2 (Sort + Hash Set, Time Complexity: $O(M*N*Log(N))$, Space Complexity: $O(M*N)$ (M: the average length of each element in `folder`, N: the number of the elements in `folder`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn remove_subfolders(mut folder: Vec<String>) -> Vec<String> {
        let n: usize = folder.len();
        folder.sort();
        let mut parent_folders: HashSet<String> = HashSet::new();
        let mut result: Vec<String> = Vec::new();
        for index_start in 0..n {
            let slashes: Vec<usize> = folder[index_start].chars().enumerate().filter(|(_, character)| *character == '/').map(|(index, _)| index).collect::<Vec<usize>>();
            let mut is_sub: bool = false;
            for index_slash in slashes {
                if parent_folders.contains(&folder[index_start][0..index_slash]) {
                    is_sub = true;
                    break;
                }
            }

            parent_folders.insert(folder[index_start].clone());

            if is_sub {
                continue;
            }
            result.push(folder[index_start].clone());
        }

        return result
    }
}
```

Method 3 (Sort + Hash Set, Time Complexity: $O(M*N*Log(N))$, Space Complexity: $O(M*N)$ (M: the average length of each element in `folder`, N: the number of the elements in `folder`)) :
```rust
use std::collections::HashSet;

impl Solution {
    pub fn remove_subfolders(mut folder: Vec<String>) -> Vec<String> {
        let n: usize = folder.len();
        folder.sort();
        let mut parent_folders: HashSet<&str> = HashSet::new();
        let mut result: Vec<String> = Vec::new();
        for index_start in 0..n {
            let slashes: Vec<usize> = folder[index_start].chars().enumerate().filter(|(_, character)| *character == '/').map(|(index, _)| index).collect::<Vec<usize>>();
            let mut is_sub: bool = false;
            for index_slash in slashes {
                if parent_folders.contains(&folder[index_start][0..index_slash]) {
                    is_sub = true;
                    break;
                }
            }

            parent_folders.insert(&folder[index_start].as_str());

            if is_sub {
                continue;
            }
            result.push(folder[index_start].clone());
        }

        return result
    }
}
```
