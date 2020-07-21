## Challenges

- [x] Find the Corrupt Pair
- [x] Find the Smallest Missing Positive Number
- [ ] Find the First K Missing Positive Numbers

## Phrases for Algorithm Description

- Problems involving arrays containing numbers in a given range
- Iterate the array one number at a time. If the current number we are iterating is not at the correct index, we swap it with the number at its correct index. This way we will go through all numbers and place them in their correct indices, hence, sorting the whole array.
- We are not incrementing the index `i` when swapping the numbers, this will result in more than `n` iterations of the loop, but in the worst-case scenario, the `while` loop will swap a total of `n-1` numbers and once a number is at its correct index, we will move on the next number by incrementing `i`.
- Say we are at index `i`, if we swap the number at index `i` to place it at the correct index, we can still have the wrong number at index `i`. This was true in Cyclic Sort too. It didn't cause any problems in Cyclic as over there, we made sure to place one number at its correct place in each step, but that wouldn't be enough in this problem as we have one extra number due to the larger range. 
- Since there is only one duplicate, if while swapping the number with its index both the numbers being swapped are same, we have found our duplicate!
- While doing the cyclic sort, we realized that the array will have a cycle due to the duplicate number and that the start of the cycle will always point to the duplicate number.
  - => Fast & Slow Pointer method doesn't modify the input array.
- The numbers are not bound by any range so we can have any number in the input array. But we can still follow the pattern of Cyclic Sort to place the numbers on their correct indices and ignore all numbers that are out of the range of the array.
  - ignore means leave them their untouched
- To handle this, we must keep track of all numbers from those indices that have missing numbers. 

## Syntax

```java
private static void swap(int[] arr, int i, int j) {
  int temp = arr[i];
  arr[i] = arr[j];
  arr[j] = temp;
}
```

```java
int i = 0;
while (i < nums.length) {
  // Take care of missing and duplication at the same time
  if (nums[i] != nums[nums[i] - 1]) 
    swap(nums, i, nums[i] - 1);
  else
    i++;
}
```

```java
new int[] { -1, -1 };
```



## Best Practices

- Sort in-place in `O(n)`

- `Item = index` or `item = index + 1`

- Allowed to modify original array or not

- ```java
  int i = 0;
  while (i < nums.length) {
    if (nums[i] > 0 && nums[i] <= nums.length && nums[i] != nums[nums[i] - 1])
      swap(nums, i, nums[i] - 1);
    else
      i++;
  }
  ```

- 

## Mistakes

- Out of range => can be negative or very large
- We are not ensured to find K missing numbers from the array. We need to add additional numbers to the output array.

## Abstraction

- 

