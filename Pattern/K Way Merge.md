## Challenges

- [x] K Pairs with Largest Sums


## Phrases for Algorithm Description

- We can push the first element of each sorted array in a Min Heap to get the overall minimum. While inserting elements to the Min heap we keep track of which array the element came from. We can, then, remove the top element from the heap to get the smallest element and push the next element from the same array, to which this smallest element belonged, to the heap. We can repeat this process to make a sorted traversal of all elements.
- If we have to find the smallest element of all the input lists, we have to compare only the first elements of each list. Once we have the smallest element, we can put it in the merged list. Following a similar pattern, we can then find the next smallest element of all the lists to add it to the merged list.
- Instead of inserting numbers into a merged list, we will keep count to see how many elements have heen inserted in the merged list. Once that count is equal to `K`, we have found our required number.
- A big difference is that in this problem, the input is a list of `arrays` compared to `LinkedLists`. This means that when we want to push the next number in the heap we need to know what the index of the current number in the current array was. To handle this, we will need to keep track of the array and the element indices.
- As each row (or column) of the given matrix can be seen as a sorted list, we **essentially** need to find the Kth smallest number in `N` sorted lists.
- In a **loop**, we'll take the smallest element from the min-heap and `currentMaxNumber` has the largest element that we inserted in the heap. If these two numbers give us a smaller range, we'll update our range. Finally, if the array of the top element has more elements, we'll insert the next element to the heap.
- **We can finish searching the minimum range as soon as** an array is completed or, in other terms, the heap has less than `M` elements.
- Since, at most, we'll be **going through** all the elements of all the arrays and will remove/add one element in the heap **in each step**, the time complexity will be `O(N*logN)` where N is the total number of elements in all the `M` input arrays.
- We can optimize our algorithm in two ways:
  - Instead of iterating over all the numbers of both arrays, we can iterate only the first `K` numbers from both arrays. Since the arrays are sorted in descending order, the pairs with the maximum sum will be constituted by the first `K` numbers from both the arrays.
  - **As soon as we encounter a pair** with a sum that is smaller than the smallest (top) element of the heap, **we don' t need to process the next elements** of the array (`break;`). Since the arrays are sorted in descending order, we won' t be able to find a pair with a higher sum moving forward.

## Syntax

```java
return new ArrayList<>(minHeap);
```

## Best Practices

- ```java
  ListNode resultHead = null, resultTail = null;
  while (!minHeap.isEmpty()) {
  ListNode node = minHeap.poll();
    if (resultHead == null) {
      resultHead = resultTail = node;
    } else {
      resultTail.next = node;
      resultTail = resultTail.next;
    }
    if (node.next != null)
      minHeap.add(node.next);
  }
  ```
  
  - `resultHead`, `resultTail`
  
- ```java
  class Node {
    int elementIndex;
    int arrayIndex;
  
    Node(int elementIndex, int arrayIndex) {
      this.elementIndex = elementIndex;
      this.arrayIndex = arrayIndex;
    }
  }
  
  int numberCount = 0, result = 0;
  while (!minHeap.isEmpty()) {
    Node node = minHeap.poll();
    result = lists.get(node.arrayIndex)[node.elementIndex];
    if (++numberCount == k)
      break;
    node.elementIndex++;
    if (lists.get(node.arrayIndex).length > node.elementIndex)
      minHeap.add(node);
  }
  return result;
  ```

  - A node is like a placeholder for an array

- 

## Mistakes

- ```java
  for (ListNode root : lists)
    if (root != null)
      minHeap.add(root);
  
  for (int i = 0; i < lists.size(); i++)
    if (lists.get(i) != null)
      minHeap.add(new Node(0, i));
  ```

  - always check existence before usage

- 

## Abstraction

- Involve a list of sorted arrays => utilize the fact that the input lists are individually sorted.
- 

