![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1282. [Group The People Given The Group Size They Belong To](https://leetcode.com/problems/group-the-people-given-the-group-size-they-belong-to)

### Solution :

Method 1 (Hash Table) :
```rust
use std::collections::HashMap;
impl Solution {
    pub fn group_the_people(group_sizes: Vec<i32>) -> Vec<Vec<i32>> {
        let mut groups: HashMap<i32, Vec<i32>> = HashMap::new();
        let mut result: Vec<Vec<i32>> = vec![];
        for (index, &size) in group_sizes.iter().enumerate() {
            (*groups.entry(size).or_insert(vec![])).push(index as i32);
            if (groups[&size].len() as i32) < size {
                continue;
            }

            result.push(groups[&size].clone());
            groups.remove(&size);
        }

        return result
    }
}
```

Method 2 (Hash Table) :
```rust
use std::collections::HashMap;
impl Solution {
    pub fn group_the_people(group_sizes: Vec<i32>) -> Vec<Vec<i32>> {
        let mut groups: HashMap<i32, Vec<i32>> = HashMap::new();
        let mut result: Vec<Vec<i32>> = vec![];
        for (index, &size) in group_sizes.iter().enumerate() {
            (*groups.entry(size).or_insert(vec![])).push(index as i32);
            if (groups[&size].len() as i32) < size {
                continue;
            }

            result.push(groups.remove_entry(&size).unwrap().1);
        }

        return result
    }
}
```

### Solution :

Method 1 (Brute Force) :
```python
class Solution:
    def groupThePeople(self, group_sizes: List[int]) -> List[List[int]]:
        peoples = [[size, index] for index, size in enumerate(group_sizes)]
        peoples.sort()

        result = []
        while peoples:
            group = [peoples.pop()]
            if group[0][0] > 1:
                for _ in range(group[0][0]-1):
                    group.append(peoples.pop())

            result.append([index for _, index in group])

        return result
```

Method 2 (Hash Table) :
```python
class Solution:
    def groupThePeople(self, group_sizes: List[int]) -> List[List[int]]:
        groups = defaultdict(list)
        result = []
        for index, size in enumerate(group_sizes):
            groups[size].append(index)
            if len(groups[size]) < size:
                continue

            result.append(groups[size])
            groups[size] = []

        return result
```

### Solution :

Method 1 (Hash Table) :
```php
class Solution {

    /**
     * @param Integer[] $groupSizes
     * @return Integer[][]
     */
    function groupThePeople(Array $groupSizes) : Array {
        $groups = [];
        $result = [];
        foreach ($groupSizes as $index => $size) {
            if (!isset($groups[$size])) {
                $groups[$size] = [];
            }

            $groups[$size][] = $index;
            if (count($groups[$size]) === $size) {
                $result[] = $groups[$size];
                unset($groups[$size]);
            }
        }

        return $result;
    }
}
```
