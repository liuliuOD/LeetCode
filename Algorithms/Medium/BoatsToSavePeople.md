![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 881. [Boats To Save People](https://leetcode.com/problems/boats-to-save-people)

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N*Log(N))$ (N: length of `people`), Space Complexity: $O()$ (doesn't use any extra space, so the `SC` depends on the implementation of each programming language, eg: Java -> $O(Log(N))$, C++ -> $O(Log(N))$, Python -> $O(N)$)) :
```python
class Solution:
    def numRescueBoats(self, people: List[int], limit: int) -> int:
        people.sort()
        left = 0
        right = len(people) - 1
        result = 0
        while left <= right:
            weight = people[left] + people[right] if left < right else people[left]
            # Option 1
            if weight > limit:
                result += 1
                right -= 1
            elif weight <= limit:
                result += 1
                right -= 1
                left += 1
            """
            # Option 2

            result += 1
            right -= 1
            if weight <= limit:
                left += 1
            """

        return result
```

Method 2 (Two Pointer + Counting Sort, Time Complexity: $O(N)$, Space Complexity: $O(MAX(M, N))$ (M: value of `limit`, N: length of `people`)) :
```python
class Solution:
    def numRescueBoats(self, people: List[int], limit: int) -> int:
        people = self.countingSort(people, limit)

        left = 0
        right = len(people) - 1
        result = 0
        while left <= right:
            weight = people[left] + people[right] if left < right else people[left]
            result += 1
            right -= 1
            if weight <= limit:
                left += 1

        return result

    def countingSort(self, people: List[int], limit: int) -> List[int]:
        counter = [0] * (limit + 1)
        for weight in people:
            counter[weight] += 1

        prefix_sum = [0] * (limit + 1)
        for weight in range(1, len(prefix_sum)):
            prefix_sum[weight] = prefix_sum[weight-1] + counter[weight]

        result = [0] * len(people)
        for weight in reversed(range(1, len(prefix_sum))):
            while prefix_sum[weight] - prefix_sum[weight-1] > 0:
                prefix_sum[weight] -= 1
                result[prefix_sum[weight]] = weight

        return result
```

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(N*Log(N))$ (N: length of `people`), Space Complexity: $O()$ (doesn't use any extra space, so the `SC` depends on the implementation of each programming language, eg: Java -> $O(Log(N))$, C++ -> $O(Log(N))$, Python -> $O(N)$, Go -> $O(1)$)) :
```go
func numRescueBoats(people []int, limit int) int {
    /* Option 1 */
    sort.Ints(people)
    /* Option 2

    slices.Sort(people)
    */
    left, right := 0, len(people)-1
    var result int = 0
    for left <= right {
        weight := people[left]
        if left != right {
            weight += people[right]
        }

        if weight <= limit {
            left++
        }
        right--
        result++
    }

    return result
}
```
