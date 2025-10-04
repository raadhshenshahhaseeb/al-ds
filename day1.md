## 147. Insertion Sort List
```
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func insertionSortList(head *ListNode) *ListNode {
	if head == nil || head.Next == nil {
		return head
	}

	temp := &ListNode{Next: head}
    lastSorted := head
    curr := head.Next

	for curr != nil {
		if lastSorted.Val <= curr.Val{
            lastSorted = curr
            curr = curr.Next
            continue
        }

        prev := temp
        for prev != lastSorted && prev.Next.Val <= curr.Val {
            prev = prev.Next
        }

        next := curr.Next
        lastSorted.Next = next
        curr.Next = prev.Next
        prev.Next = curr

        curr = next
	}

    return temp.Next
}
```
