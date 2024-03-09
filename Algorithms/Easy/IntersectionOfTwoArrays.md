![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 349. [Intersection Of Two Arrays](https://leetcode.com/problems/intersection-of-two-arrays)

### Solution :

Method 1 (Brute Force, Time Complexity: $O(M*N)$ (M: length of `nums1`, N: length of `nums2`), Space Complexity: $O(N)$) :
```go
func intersection(nums1 []int, nums2 []int) []int {
    var result []int
    for _, num1 := range nums1 {
        for _, exist := range result {
            if num1 == exist {
                goto Skip
            }
        }
        for _, num2 := range nums2 {
            if num1 == num2 {
                result = append(result, num1)
                break
            }
        }
Skip:
    }

    return result
}
```

Method 2 (Hash Map, Time Complexity: $O(M+N)$ (M: length of `nums1`, N: length of `nums2`), Space Complexity: $O(M+N)$) :
```go
func intersection(nums1 []int, nums2 []int) []int {
    set1, set2 := make(map[int]bool), make(map[int]bool)
    for _, num := range nums1 {
        set1[num] = true
    }
    for _, num := range nums2 {
        set2[num] = true
    }

    result := []int{}
    for key, _ := range set1 {
        _, ok := set2[key]
        if ok {
            result = append(result, key)
        }
    }

    return result
}
```

Method 3 (Hash Map, Time Complexity: $O(M+N)$ (M: length of `nums1`, N: length of `nums2`), Space Complexity: $O(M)$) :
```go
func intersection(nums1 []int, nums2 []int) []int {
    set1 := make(map[int]bool)
    for _, num := range nums1 {
        set1[num] = true
    }

    result := []int{}
    for _, num := range nums2 {
        _, ok := set1[num]
        if !ok {
            continue
        }

        result = append(result, num)
        delete(set1, num)
    }

    return result
}
```

Method 4 (Sort + Two Pointer, Time Complexity: $O(M*Log(M)+N*Log(N))$ (M: length of `nums1`, N: length of `nums2`), Space Complexity: $O(M+N)$) :
```go
func intersection(nums1 []int, nums2 []int) []int {
    sort.Ints(nums1)
    sort.Ints(nums2)
    var result []int
    for pointer1, pointer2 := 0, 0; pointer1 < len(nums1) && pointer2 < len(nums2); {
        if nums1[pointer1] == nums2[pointer2] {
            if result == nil || nums1[pointer1] > result[len(result)-1] {
                result = append(result, nums1[pointer1])
            }
            pointer1++
            pointer2++
        } else if nums1[pointer1] < nums2[pointer2] {
            pointer1++
        } else {
            pointer2++
        }
    }

    return result
}
```
