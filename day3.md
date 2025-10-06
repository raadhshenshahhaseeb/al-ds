# Introduction to Algorithm(Cormen) - Day 3 (Chapter 2 + Leetcode)
## 21. Merge Two Sorted Lists

#### Sol 1
If either list is empty, return the other list.
Compare `list1.Val` wand `list2.Val` and pick the smaller head.
After picking the first, remainder nodes of the list are recursively attached.

```
func mergeTwoLists(list1 *ListNode, list2 *ListNode) *ListNode {
    // if either list is empty, the merged list is the other one.
    if list1 == nil { return list2 }
    if list2 == nil { return list1 }

    if list1.Val <= list2.Val {
        list1.Next = mergeTwoLists(list1.Next, list2)
        return list1
    }
    list2.Next = mergeTwoLists(list1, list2.Next)
    return list2
}
```

#### Sol 2
For each iteration, the portion from `dummy.Next` to `tail` is a correctly merged and sorted prefix of the overall result.
All unmerged nodes are exactly those in `list1` and `list2`.
The next node to append must be smaller of the 2 heads.

```
func mergeTwoLists(list1 *ListNode, list2 *ListNode) *ListNode {
    dummy := &ListNode{}
    tail := dummy
    for list1 != nil && list2 != nil {
        if list1.Val <= list2.Val {
            tail.Next = list1
            list1 = list1.Next
        } else {
            tail.Next = list2
            list2 = list2.Next
        }
        tail = tail.Next
    }
    if list1 != nil { tail.Next = list1 } else { tail.Next = list2 }
    return dummy.Next
}

```

#### Time/Space Complexity(Both)
**Time Complexity:** `O(n+m)`

`n = length of list1`, `m = length of list2`

Overall work is linear in the total number of nodes. Each step removes exactly one node from the selection.

**Space Complexity:**

**For recursive:** `O(n+m) in worst case` because every time a function calls itself, it has to return after the inner call returns. 
**For iterative:** `O(1)` because we only keep few pointers and this extra memory stays constant irrespective of the list size.

## 912. Sort an Array
```
func sortArray(nums []int) []int {
	if len(nums) == 0 {
		return nums
	}

	buf := make([]int, len(nums))
	mergeSort(nums, buf, 0, len(nums))
	return nums
}

func mergeSort(a, buf []int, l, r int) {
	if r-l <= 1 {
		return
	}
	m := l + (r-l)/2
	mergeSort(a, buf, l, m)
	mergeSort(a, buf, m, r)
	mergeRange(a, buf, l, m, r)
}

func mergeRange(a, buf []int, l, m, r int) {
	i, j, k := l, m, l
	for i < m && j < r {
		if a[i] <= a[j] {
			buf[k] = a[i]
			i++
		} else {
			buf[k] = a[j]
			j++
		}
		k++
	}
	for i < m {
		buf[k] = a[i]
		i++
		k++
	}
	for j < r {
		buf[k] = a[j]
		j++
		k++
	}
	for t := l; t < r; t++ {
		a[t] = buf[t]
	}
}


```
