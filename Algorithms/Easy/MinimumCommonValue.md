![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 2540. [Minimum Common Value](https://leetcode.com/problems/minimum-common-value)

### Solution :

Method 1 (Two Pointer, Time Complexity: $O(M+N)$ (M: length of `nums1`, N: length of `nums2`), Space Complexity: $O(1)$) :
```go
func getCommon(nums1 []int, nums2 []int) int {
    n1, n2 := len(nums1), len(nums2)
    pointer1, pointer2 := 0, 0
    for pointer1 < n1 && pointer2 < n2 {
        if nums1[pointer1] == nums2[pointer2] {
            return nums1[pointer1]
        } else if nums1[pointer1] < nums2[pointer2] {
            pointer1++
        } else {
            pointer2++
        }
    }

    return -1
}
```
