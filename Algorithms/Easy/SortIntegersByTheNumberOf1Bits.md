![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1356. [Sort Integers By The Number Of 1 Bits](https://leetcode.com/problems/sort-integers-by-the-number-of-1-bits)

### Solution :

Method 1 :
```rust
impl Solution {
    pub fn sort_by_bits(mut arr: Vec<i32>) -> Vec<i32> {
        /* Option 1 */
        arr.sort_by_key(|&item| ((item as usize).count_ones(), item));
        /* Option 2

        arr.sort_by_key(|&item| (item.count_ones(), item));
        */
        return arr
    }
}
```

### Solution :

Method 1 (Built-In Function) :
```python
class Solution:
    def sortByBits(self, arr: List[int]) -> List[int]:
        return sorted(arr, key=lambda item: (bin(item).count('1'), item))
```

Method 2 (Brute Force, Time Complexity: $O(N^2)$) :
```python
class Solution:
    def sortByBits(self, arr: List[int]) -> List[int]:
        arr_temp = [[item for item in arr if bin(item).count('1') == bit] for bit in range(15)]
        arr_temp = map(lambda group: sorted(group), arr_temp)
        result = []
        for group in arr_temp:
            result += group

        return result
```

Method 3 (Hash Map, Time Complexity: $O(M*N*Log(N))$ (M: number of bit, N: length of arr)) :
```python
class Solution:
    def sortByBits(self, arr: List[int]) -> List[int]:
        mapping = defaultdict(list)
        for item in arr:
            mapping[bin(item).count('1')].append(item)

        result = []
        for key in sorted(mapping.keys()):
            result += sorted(mapping[key])

        return result
```

Method 4 (Hash Map + Binary Heap, Time Complexity: $O(N*Log(N))$) :
```python
class Solution:
    def sortByBits(self, arr: List[int]) -> List[int]:
        mapping = defaultdict(list)
        for item in arr:
            heapq.heappush(mapping[bin(item).count('1')], item)

        result = []
        for key in sorted(mapping.keys()):
            while mapping[key]:
                result.append(heapq.heappop(mapping[key]))

        return result
```
