## Challenges

- [x] Next Interval

- [ ] 

## Phrases for Algorithm Description

- We are interested in knowing the smallest element in one part and the biggest element in the other part. This pattern uses two heaps to solve these problems: A min heap to find the smallest element and a max heap to find the biggest element.
- Inserting a number in a sorted list will take `O(N)` time if there are `N ` numbers in the list.
- Utilize the fact that we don't need the fully sorted list - we are only interested in finding the middle element.
- Two Heaps:
  - Store the first half of numbers in a **Max Heap**. 
  - Store the second half of numbers in a **Min Heap**.
  - Inserting a number in a heap will take **O(logN)**, which is better than the brute force approach.
  - At any time, the median of the current list of numbers can be calculated from the top element of the two heaps.
  - Either both the heaps will have equal number of elements or max-heap will have one more element than the min-heap.
  - The space complexity will be `O(N)` because, as at any time, we will be storing all the numbers.
- The only difference is that we need to keep track of a sliding window of `k` numbers. This means, in each iteration, when we insert a new number in the heaps, we need to remove one number from the heaps which is going out of the sliding window. After the removal, we need to rebalance the heaps in the same way that we did while inserting.
- The time complexity is `O(N*K)`
  - Inserting/removing numbers from heaps of size `K`. This will take `O(logK)`
  - Removing the element going out of the sliding window. This will take `O(K)` as we will be searching this element in an array of size `K`
- Ignoring the space needed for ...
- Since, at the most, all the projects will be pushed to both the heaps once, the time complexity of our algorithm is `O(NlogN + KlogN)`, where `N` is the total number of projects and `K` is the number of projects we are selecting.
- It is given that none of the intervals have the same start point.
- We can push all intervals into two heaps: one heap to sort the intervals on maximum start time and the other on maximum end time. We can then iterate through all intervals of the `maxEndHeap` to find their next interval.
  - Take out the top interval from the `maxEndHeap` to find its next interval `topEnd`
  - Find an interval in the `maxStartHeap` with the closest start greater than or equal to the start of `topEnd`, `topStart`.
  - Add the index of topStart in the result array as the next interval of `topEnd`. If we can't find the next interval, add `-1` in the result array.
  - Put `topStart` back into `maxStartHeap`, as it could be the next interval of other intervals.
    - But those popped out during the process of finding `topStart` are useless and can be throw away.

## Syntax

```java
maxHeap = new PriorityQueue<>((a, b) -> b - a);
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
if (maxHeap.isEmpty() || maxHeap.peek() >= num){}
maxHeap.remove(elementToBeRemoved);
PriorityQueue<Integer> maxProfitHeap = new PriorityQueue<>(n, (i1, i2) -> profits[i2] - profits[i1]);
```



## Best Practices

- ```java
  while (!minCapitalHeap.isEmpty() && capital[minCapitalHeap.peek()] <= availableCapital){}
  ```

- 

## Mistakes

- Terminate if we are not able to find any project that can be completed within the available capital.

## Abstraction

- 

