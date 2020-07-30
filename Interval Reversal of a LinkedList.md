## Challenges

- [x] Reverse alternating K-element Sub-list
- [x] Rotate a LinkedList

- [ ] 

## Phrases for Algorithm Description

- Reverse the links between a set of nodes of a LinkedList, using the existing node objects and without using extra memory.
- To reverse a LinkedList, we need to reverse one node at a time. We will start with a variable `current` which will initially point to the head of the LinkedList, a variable `previous` which will point to the previous node that we have processed and a variable `next` which will be used to temporarily store the next node. Initially `previous` will point to `null`. 
- In a stepwise manner, we will reverse the `current` node by pointing it to the `previous` before moving on to the next node. Also, we will update the `previous` to always point to the previous node that we have processed.
- After the loop current will be pointing to `null` and `previous` will be the new head.
- Remember the node at position `p-1` to be used later to connect with the reversed sublist.
- Connect the `p-1` and `q+1` nodes to the reversed sub-list.
- After reversing the LinkedList `current` will become the last node of the sub-list
- When 'n' is even we can perform the following steps; when 'n' is odd, our algorithm will look like.
- Please note the function call in the seconde step. We're skipping two elements as we will be skipping the middle element.
- We can follow a similar approach, and in each iteration after reversing `k` elements, we will skip the next `k` elements
  - *Instead of using a flag*

## Syntax

```java
if (p == q)
  return head;
```

```java
if (k <= 1 || head == null)
  return head;
```



## Best Practices

- It's always better to do less traversal

  - Remember the last node of sub-list in advance
  - Remember `p-1` while locating `p`
  - After the `while-loop` of reversion, current will be pointing to a node outside sub-list

- Write the `for-loop` first, then verify boundary conditions

- Check null before access the  `next` pointer of list node

- Take care of the case when left with a sub-list with less than `k` elements.

- ``` java
  while (true) {
    ListNode lastNodeOfPreviousPart = previous;
    ListNode lastNodeOfSubList = current;
    ListNode next = null;
    for (int i = 0; current != null && i < k; i++) {
      next = current.next;
      current.next = previous;
      previous = current;
      current = next;
    }
    if (lastNodeOfPreviousPart != null) {
      lastNodePreviousPart.next = previous;
    } else {
      head = previous;
    }
    lastNodeOfSubList.next = current;
    if (current == null) {
      break;
    }
  }
  ```

- 

## Mistakes

- 

## Abstraction

- 

