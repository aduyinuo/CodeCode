## Challenges

- [x] Search in bitonic array
- [x] Search in rotated array

## Phrases for Algorithm Description

- Binary Search
  - `start` is pointing to the first index and `end` is pointing to the last index of the input array
  - find the `middle` of `start` and `end`. 
  - see if the `key` is equal to the number at index `middle`. 
    - If it is equal return `middle` as the required index
    - If not equal, check `key < arr[middle]` or `key > arr[middle]`
    - reduce search range accordingly
  - Since the loop is running until `start <= end`, at the end of the while loop, `start = end + 1`, which suggests we are not able to find the element in the given array.
  - Since, we are reducing the search range by half at every step, this means that the time complexity of our algorithm will be `O(logN)` where `N` is the total elements in the given array. The algorithm runs in constant space `O(1)`
- We can add a check in the beginning to see if the `key` is bigger than the biggest number in the input array. If so, we can return `-1`.
- An efficient way to find the proper bounds is to start at the beginning of the array with the bound's size as `1` and exponentially increase the bound's size (i.e., double it) untill we find the bounds that can have the key.
- There are two parts of the algorithm. In the first part, we keep increasing the bound's size exponentially (double it every time) while searching for the proper bounds. 
- Find the index of the maximum value of the bitonic array, break the array into two sub-arrays and search seperately in these two arrays.
- After calculating the middle, we can compare the numbers at indices `start` and `middle`. It will tell us which part of the array is in ascending order.
- If numbers at indexes start, mid and end are same, we can't choose a side. The best we can do, is to skip one number from both ends as `key ~= arr[mid]`

## Syntax

```java

```

## Best Practices

- ```java
  middle  = start + (end-start)/2
  ```

  - Avoid integer overflow

- ```java
  if (key < letters[0] || key > letters[n - 1])
    return letters[0];
  ```

  - cross out illegal cases at the beginning

- no need to search for upper limit, if `key` is not present in the input array 

- ```java
  public static int search(ArrayReader reader, int key) {
    // find the proper bounds first
    int start = 0, end = 1;
    while (reader.get(end) < key) {
      int newStart = end + 1;
      end += (end - start + 1) * 2; // increase to double the bounds size
      start = newStart;
    }
    return binarySearch(reader, key, start, end);
  }
  ```

  - beautiful and clever

- no need to search again in the second subarray if already found in the first part.

## Mistakes

- sort in ascending or descending order
- what if we can't find the key? or the index with required attributes?
- assume the given array is a circular list?
- Monotonically?
- return index or the element itself?
- duplicates allowed?

## Abstraction

- Find sorted range
- Determine target attributes
- clarify above factors

