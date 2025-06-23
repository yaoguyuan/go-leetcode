# LC2 - 两数相加

```go title="AddTwoNumbers.go" linenums="1" hl_lines="14 18"
package LinkedList

func addTwoNumbers(l1 *ListNode, l2 *ListNode) *ListNode {
	virtualHead := new(ListNode)
	tail := virtualHead
	carry := 0
	for l1 != nil || l2 != nil {
		if l1 == nil {
			l1 = new(ListNode)
		}
		if l2 == nil {
			l2 = new(ListNode)
		}
		sum := (l1.Val + l2.Val + carry) % 10
		tail.Next = new(ListNode)
		tail = tail.Next
		tail.Val = sum
		carry = (l1.Val + l2.Val + carry) / 10
		l1 = l1.Next
		l2 = l2.Next
	}
	if carry == 1 {
		tail.Next = new(ListNode)
		tail = tail.Next
		tail.Val = 1
	}
	return virtualHead.Next
}
```

通过创建虚拟节点，模拟位数不足时的高位补零。