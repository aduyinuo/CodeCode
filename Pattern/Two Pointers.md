## Challenges

- [x] Quadruple Sum to Target
- [x] Comparing Strings containing backspaces (start from the end to help apply backspace)
- [x] Minimum Window Sort

## Phrases for Algorithm Description

- **Consider** each element one by one
- **Given that** the input array is sorted, **an efficient way would be to** **start with** one pointer in the beginning and another pointer at the end.
- If, this means. So, to try more pairs, we can decrement the end-pointer.
- A brute-force solution could be to iterate through the array, taking one number at a time...
- We can utilize a HashTable to search for the required pair. 
- During our iteration, we are at number X, so we need to find Y such that X + Y == Target.
- Search for Y in the HashTable. If it is there, we have found the required pair.
- Otherwise, insert X in the HashTable, so that we can search it for the later numbers.
- Keep one pointer for iterating the array and one pointer for placing the next non-duplicate number.
- Iterate the array and whenever we see a non-duplicate number we move it next to the last non-duplicate number we've seen.
- Find the index of the first non-negative number in the array。
- We can use two pointers to iterate the array. One pointer will move forward and the other pointer will move backward.
- **At any step, whichever pointer gives us the bigger square we add it to the result array and move to the next position.**
- **The main `for-loop` managing the sliding window** takes `O(N)` but creating subarrays can take up to O(N^2) in the worst case. Therefore overall, our algorithm will take O(N^3)
- **Ignoring the space required for** the output list, **the algorithm runs in O(N) space** **which is used for** the temp list.
- For an array with distinct elements, finding all of its contiguous subarrays is like finding the number of ways to choose two indicies i and j in the array such that `i <= j` 
- Let's say the two pointers are called `low` and `high` which are pointing to the first and the last element of the array respectively. So while iterating, we will move all 0s before `low` and all 2s after `high` so that in the end, all 1s will be between `low` and `high`
- The time complexity will be `O(N)` as we are iterating the input array only once.
- The time complexity of the above algorithm will be `O(M+N)` where M and N are the lengths of the two input strings respectively.
- Find the length of the smallest subarray which when sorted will sort the whole array.
- From the beginning and end of the array, find the first elements that are out of sorting order. The two elements will be our candidate subarray.
- Find the maximum and minimum of this subarray.
- Extend the subarray from beginning to include any number which is bigger than the minimum of the subarray.
- Similarly, extend the subarray from the end to include any number which is smaller than the maximum of the subarray.

## Syntax

```java
tempList.add(0, arr[i]);
result.add(new ArrayList<>(tempList));
```

```java
private static void swap(int[] arr, int i, int j) {
	int temp = arr[i];
	arr[i] = arr[j];
	arr[j] = temp;
}
```

```java
quadruplets.add(Arrays.asList(arr[first], arr[second], arr[left], arr[right]));
```

```java
Stack<Character> stack = new Stack<Character>();
StringBuffer sb = new StringBuffer();
sb.append();
sb.reverse();
sb.toString();
```

```java
private static int getNextValidCharIndex(String str, int index) {
    int backspaceCount = 0;
    while (index >= 0) {
      if (str.charAt(index) == '#') // found a backspace character
        backspaceCount++;
      else if (backspaceCount > 0) // a non-backspace character
        backspaceCount--;
      else
        break;

      index--; // skip a backspace or a valid character
    }
    return index;
  }
```



## Best Practices

- Try to think in the opposite way:
  - The possible zero in the middle can give us the smallest square. 
  - => The numbers at both the ends can give us the largest square.
- Always check if the input array is sorted
- Take care of the `unique` requirement
- To meet the condition `i != j != k` we need to make sure that each number is not used more than once.
- Sort the array => all the duplicate numbers will be next to each other and are easier to skip
- If there are more than one such triplet, go with the triplet with smallest sum
- `distance`
- contiguous subarray => slide windows-ish two pointers; pair/triplet => opposite two pointers
- Sorting requirement: **In-Place**
- write a swap function for sorting algorithms
- stack is perfect for reverse

## Mistakes

- Length = max index + 1
- Unique triplets problem: 
  - for a X, search for its Y and Z only from right subarray. No need to consider left part, which will cause duplicate.
  - Only dedup when a triplet is found
- Triplet Sum Close to Target
  - Update condition: Smaller distance / Same distance + Smaller sum
- Triplet with Smaller Sum
  - Strictly smaller
  - Sort the input array
- Subarray with Product Less than a Target 
  - Subarrays with inclusion relationship are all included
- *Time complexity of `new ArrayList<>(tempList)` ?*
- The answer doesn't have to exist
- `for (int i = 0; i < arr.length && i <= candidateStart; i++)`
  - CAN NOT assume candidateStart < arr.length

## Abstraction

Iteration = Start Point + Direction + Speed

- Start Point: 0, middle, arr.length - 1
- Direction: Forward, Backward
- Speed: `getNextValidCharIndex`

### LeetCode

- [x] K-diff Pairs in an Array

  - ```java
    class Solution {
        public int findPairs(int[] nums, int k) {
            Arrays.sort(nums);
            int cnt = 0;
            int large = 1, small = 0;
            while (large < nums.length) {
                if (small >= large) {
                    large++;
                    continue;
                }
                
                int diff = nums[large] - nums[small];
                if (diff > k) {
                    small++;
                } else if (diff < k) {
                    large++;
                } else {
                    cnt++;
                    small++;
                    while (small < nums.length && nums[small] == nums[small - 1]) {
                        small++;
                    }
                }
            }
            
            return cnt;
        }
    }
    ```

  - Notice how we update pointer small for deduplication

- [x] 4Sum

  - ```java
    public List<List<Integer>> fourSum(int[] nums, int target) {
        Arrays.sort(nums);
        return kSum(nums, target, 0, 4);
    }
    public List<List<Integer>> kSum(int[] nums, int target, int start, int k) {
        List<List<Integer>> res = new ArrayList<>();
        if (start == nums.length || nums[start] * k > target || target > nums[nums.length - 1] * k)
            return res;
        if (k == 2)
            return twoSum(nums, target, start);
        for (int i = start; i < nums.length; ++i)
            if (i == start || nums[i - 1] != nums[i])
                for (var set : kSum(nums, target - nums[i], i + 1, k - 1)) {
                    res.add(new ArrayList<>(Arrays.asList(nums[i])));
                    res.get(res.size() - 1).addAll(set);
                }
        return res;
    }
    public List<List<Integer>> twoSum(int[] nums, int target, int start) {
        List<List<Integer>> res = new ArrayList<>();
        int lo = start, hi = nums.length - 1;
        while (lo < hi) {
            int sum = nums[lo] + nums[hi];
            if (sum < target || (lo > start && nums[lo] == nums[lo - 1]))
                ++lo;
            else if (sum > target || (hi < nums.length - 1 && nums[hi] == nums[hi + 1]))
                --hi;
            else
                res.add(Arrays.asList(nums[lo++], nums[hi--]));
        }
        return res;
    }
    ```

  - **K Sum Version**

- [x]  Implement strStr()

  - A good clarification question to ask => What should we return when needle is an empty string? 
  - Java string.equals

- [ ] 