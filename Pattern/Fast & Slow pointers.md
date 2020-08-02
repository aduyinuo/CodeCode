## Challenges

- [x] Palindrome LinkedList
- [x] Rearrange a LinkedList
- [x] Cycle in a Circular Array

## Phrases for Algorithm Description

- The faster pointer is bound to catch up the slower pointer from behind.
- As `pointer2` is K nodes ahead of `pointer1`, which means, `pointer2` must have completed one loop in the cycle when both pointers meet. Their meeting point will be the start of the cycle.
- We can use the Fast & Slow pointers method such that the fast pointer is always twice the nodes ahead of the slow pointer. This way, when the fast pointer reaches the end of the LinkedList, the slow pointer will be pointing at the middle node.
- This means that if we divide the LinkedList into two halves, the node values ofthe first half in the forward direction should be similar to the node values of the second half in the backward direction.

## Syntax

```java
public static ListNode findMiddle(ListNode head) {
  // TODO: Write your code here
  ListNode fast = head, slow = head;
  while (fast != null && fast.next != null) {
    fast = fast.next.next;
    slow = slow.next;
  }
  return slow;
}
```

```java
private static ListNode reverse(ListNode head) {
	ListNode prev = null;
	while (head != null) {
		ListNode next = head.next;
		head.next = prev;
		prev = head;
		head = next;
	}
	return prev;
}
```



## Best Practices

- Cyclic structure => fast & slow pointers, save space compared to `HashSet`
- store the head of reversed part to revert back later

## Mistakes

- Cycle in a Circular Array
  - **Start from each index** of the array to find the cycle, not only index 0
  - The cycle should have more than one element
  - Should follow one direction

## Abstraction

- Definition of Cycle
- Definition of Get Next
- Definition of LinkedList End

