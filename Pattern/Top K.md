## Challenges

- [x] Rearrange String K Distance Apart
- [x] Scheduling Tasks

- [x] 

## Phrases for Algorithm Description

- Iterate through the array one element at a time and keep `K` largest numbers in a heap such that each time we find a larger number than the smallest number in the heap, we do two things
  - Take out the smallest number from the heap
  - Insert the larger number into the heap
- This will ensure that we always have `K` largest numbers in the heap. The most efficient way to repeatedly find the smallest number among a set of numbers will be to use a min-heap. We can find the smallest number in a min-heap in constant time O(1), since the smallest number is always at the root of the heap. Extracting the smallest number from a min-heap will take O(logN) (if the heap has N elements) as the heap needs to readjust after the removal of an element.
- While iterating through all points, if a point `P` is closer to the origin than the top point of the max-heap, we will remove that top point from the heap and add `P` to always keep the closest points in the heap.
- To keep the resultant list sorted we can use a Queue. So whenever we take the number pointed out by the left pointer, we will append it at the beginning of the list and whenever we take the number pointed out by the right pointer we will append it at the end of the list.
- Following a greedy approach, in a stepwise fashion, we will remove the least frequent number from the heap, and try to make it distinct. 
- To make an element distinct, we need to remove all of its occurences except one.
- We can work in a stepwise fashion to create a string with all characters from the input string. Following a greedy approach, we should first append the most frequent characters to the output strings, for which we can use a Max Heap. By appending the most frequent character first, we have the best chance to find a string where no two same characters come next to each other.
- If we can append all the characters from the input string to the output string, we would have successfully found an arrangement of the given string where no two same characters appeared adjacent to each other.
- We can keep track of previous characters in a queue to insert them back in the heap after `K` iterations.

## Syntax

```java
PriorityQueue<Integer> kLarge = new PriorityQueue<Integer>();
PriorityQueue<Point> maxHeap = new PriorityQueue<>((p1, p2) -> p2.distFromOrigin() - p1.distFromOrigin());
PriorityQueue<Map.Entry<Integer, Integer>> minHeap = new PriorityQueue<Map.Entry<Integer, Integer>>(
    (e1, e2) -> e1.getValue() - e2.getValue());
for (Map.Entry<Integer, Integer> entry : numFrequencyMap.entrySet()) {
  minHeap.add(entry);
  if (minHeap.size() > k) {
    minHeap.poll();
  }
}
```

```java
maxHeap.addAll(charFrequencyMap.entrySet());

Queue<Map.Entry<Character, Integer>> queue = new LinkedList<>();
StringBuilder resultString = new StringBuilder(str.length());
```

## Best Practices

- Don't know when to use greedy approach

- ```java
  public static String rearrangeString(String str) {
    Map<Character, Integer> charFrequencyMap = new HashMap<>();
    for (char chr : str.toCharArray())
      charFrequencyMap.put(chr, charFrequencyMap.getOrDefault(chr, 0) + 1);
  
    PriorityQueue<Map.Entry<Character, Integer>> maxHeap = new PriorityQueue<Map.Entry<Character, Integer>>(
        (e1, e2) -> e2.getValue() - e1.getValue());
  
    // add all characters to the max heap
    maxHeap.addAll(charFrequencyMap.entrySet());
  
    Map.Entry<Character, Integer> previousEntry = null;
    StringBuilder resultString = new StringBuilder(str.length());
    while (!maxHeap.isEmpty()) {
      Map.Entry<Character, Integer> currentEntry = maxHeap.poll();
      // add the previous entry back in the heap if its frequency is greater than zero
      if (previousEntry != null && previousEntry.getValue() > 0)
        maxHeap.offer(previousEntry);
      // append the current character to the result string and decrement its count
      resultString.append(currentEntry.getKey());
      currentEntry.setValue(currentEntry.getValue() - 1);
      previousEntry = currentEntry;
    }
  
    // if we were successful in appending all the characters to the result string, return it
    return resultString.length() == str.length() ? resultString.toString() : "";
  }
  ```

  - The beauty of `previous` pointer

## Mistakes

- Kth smallest number in the sorted order or the Kth distinct element?
- if k > 0 after removement, we have to remove some distinct numbers
- if two numbers have the same frequency, we will need to return the number which was pushed later while popping. To resolve this, we need to attach a sequence number to every number to know which number came first.

## Abstraction

- 

