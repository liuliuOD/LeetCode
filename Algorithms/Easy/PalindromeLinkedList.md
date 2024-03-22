![language-Python](https://img.shields.io/badge/Python-ffd43b?style=for-the-badge&logo=PYTHON)
![language-Go](https://img.shields.io/badge/Go-00add8?style=for-the-badge&logo=GO&logoColor=white)
---

## 234. [Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list)

### Solution :

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
```

Method 1 (Slow & Fast Pointer + Stack) :
```python
class Solution:
    def isPalindrome(self, head: Optional[ListNode]) -> bool:
        if head.next is None:
            return True

        stack = [head.val]
        pointer_slow = head
        pointer_fast = head.next
        while pointer_fast and pointer_fast.next:
            pointer_slow = pointer_slow.next
            pointer_fast = pointer_fast.next.next

            stack.append(pointer_slow.val)

        # This means amount of nodes is odd. So use pop to drop middle node
        if pointer_fast is None:
            stack.pop()
        
        """
        Move pointer to start node of end half.
        eg: 1 -> 2 -> 3
            after while loop above, current pointer_slow = 2. So we should move to 3.
        eg: 1 -> 2 -> 3 -> 4
            should move to 3.
        """
        pointer_slow = pointer_slow.next
        while pointer_slow:
            if stack.pop() != pointer_slow.val:
                return False
            pointer_slow = pointer_slow.next
        return True
```

### Solution :

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
```

Method 1 (Array, Time Complexity: $O(N)$, Space Complexity: $O(N)$) :
```go
func isPalindrome(head *ListNode) bool {
    var list []int
    for ;head != nil; head = head.Next {
        list = append(list, head.Val)
    }

    left, right := 0, len(list)-1
    for left < right {
        if list[left] != list[right] {
            return false
        }

        left++
        right--
    }

    return true
}
```
