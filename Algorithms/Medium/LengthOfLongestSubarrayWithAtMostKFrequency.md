![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 2958. [Length Of Longest Subarray With At Most K Frequency](https://leetcode.com/problems/length-of-longest-subarray-with-at-most-k-frequency)

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```python
class Solution:
    def maxSubarrayLength(self, nums: List[int], k: int) -> int:
        counter = defaultdict(int)
        left = 0
        result = 0
        for right, num in enumerate(nums):
            counter[num] += 1
            while left <= right and counter[num] > k:
                counter[nums[left]] -= 1
                left += 1

            result = max(result, right - left + 1)

        return result
```

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```go
func maxSubarrayLength(nums []int, k int) int {
    result := 0
    left := 0
    counter := make(map[int]int)
    for right, num :=range nums {
        counter[num]++
        /* Option 1 */
        for left <= right && counter[num] > k {
        /* Option 2
        
        for counter[num] > k {
        */
            counter[nums[left]]--
            left++
        }

        if result < (right-left+1) {
            result = right - left + 1
        }
    }

    return result
}
```
