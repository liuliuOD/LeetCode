![language-RUST](https://img.shields.io/badge/%20-RUST-8d4004?style=for-the-badge&logo=RUST)
![language-Python](https://img.shields.io/badge/%20-Python-ffd43b?style=for-the-badge&logo=PYTHON)
---

## 1877. [Minimize Maximum Pair Sum In Array](https://leetcode.com/problems/minimize-maximum-pair-sum-in-array)

### Solution :

Method 1 (Built-In + Two Pointers) :
```rust
impl Solution {
    pub fn min_pair_sum(mut nums: Vec<i32>) -> i32 {
        nums.sort();
        let mut result: i32 = 0;
        let mut pointer_left: usize = 0;
        let mut pointer_right: usize = nums.len() - 1;
        while pointer_left < pointer_right {
            let pair_sum: i32 = nums[pointer_left] + nums[pointer_right];
            if pair_sum > result {
                result = pair_sum;
            }

            pointer_left += 1;
            pointer_right -= 1;
        }

        return result
    }
}
```

### Solution :

Method 1 (Built-In + Two Pointers, Time Complexity: $O(N*Log(N))$, Space Complexity: $O(N)$) :
```python
class Solution:
    def minPairSum(self, nums: List[int]) -> int:
        nums.sort()
        left = 0
        right = len(nums) - 1
        pairs_sum = []
        while left < right:
            pairs_sum.append(nums[left] + nums[right])
            left += 1
            right -= 1

        return max(pairs_sum)
```

Method 2 (Built-In + Two Pointers, Time Complexity: $O(N*Log(N))$, Space Complexity: $O()$ (doesn't use any extra space, so the `SC` depends on the implementation of each programming language)) :
```python
class Solution:
    def minPairSum(self, nums: List[int]) -> int:
        nums.sort()
        left = 0
        right = len(nums) - 1
        result = 0
        while left < right:
            pair_sum = nums[left] + nums[right]
            if result < pair_sum:
                result = pair_sum

            left += 1
            right -= 1

        return result
```

Method 3 (Binary Heap) :
```python
class Solution:
    def minPairSum(self, nums: List[int]) -> int:
        heap_min = []
        heap_max = []
        for num in nums:
            heapq.heappush(heap_min, num)
            heapq.heappush(heap_max, -num)

        n = len(nums)
        result = 0
        for _ in range(n//2):
            pair_sum = heapq.heappop(heap_min) - heapq.heappop(heap_max)
            if result < pair_sum:
                result = pair_sum

        return result
```

Method 4 (Counting Sort) :
```python
class Solution:
    def minPairSum(self, nums: List[int]) -> int:
        nums_ordered = self.countingSort(nums)

        left, right = 0, len(nums) - 1
        result = 0
        while left < right:
            pair_sum = nums_ordered[left] + nums_ordered[right]
            if result < pair_sum:
                result = pair_sum

            left += 1
            right -= 1

        return result

    def countingSort(self, nums: List[int]) -> List[int]:
        counting = [0] * 100_001
        for num in nums:
            counting[num] += 1

        prefix_sum = [counting[0]]
        for index in range(1, len(counting)):
            prefix_sum.append(prefix_sum[index-1] + counting[index])

        n = len(nums)
        nums_ordered = [0] * n
        for index in reversed(range(n)):
            prefix_sum[nums[index]] -= 1
            nums_ordered[prefix_sum[nums[index]]] = nums[index]

        return nums_ordered
```

Method 5 (Count Frequency + Dictionary) :
```python
class Solution:
    def minPairSum(self, nums: List[int]) -> int:
        # Option 1
        counting = defaultdict(int)
        minimum = inf
        maximum = -inf
        for num in nums:
            counting[num] += 1
            minimum = min(minimum, num)
            maximum = max(maximum, num)
        maximum_limit = maximum
        """
        # Option 2

        counting = Counter(nums)
        minimum = min(nums)
        maximum = maximum_limit = max(nums)
        """

        result = 0
        while minimum <= maximum:
            while minimum <= maximum_limit and (minimum not in counting or counting[minimum] <= 0):
                minimum += 1
            while maximum >= 0 and (maximum not in counting or counting[maximum] <= 0):
                maximum -= 1

            if minimum > maximum:
                break

            pair_sum = minimum + maximum
            if result < pair_sum:
                result = pair_sum

            counting[minimum] -= 1
            counting[maximum] -= 1

        return result
```

Method 6 (Count Frequency + List) :
```python
class Solution:
    def minPairSum(self, nums: List[int]) -> int:
        counting = [0] * 100_001
        minimum = inf
        maximum = -inf
        for num in nums:
            counting[num] += 1
            minimum = min(minimum, num)
            maximum = max(maximum, num)

        result = 0
        while minimum <= maximum:
            if counting[minimum] == 0:
                minimum += 1
            elif counting[maximum] == 0:
                maximum -= 1
            else:
                pair_sum = minimum + maximum
                if result < pair_sum:
                    result = pair_sum

                counting[minimum] -= 1
                counting[maximum] -= 1

        return result
```
