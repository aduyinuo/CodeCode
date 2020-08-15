## Challenges

- [x] Permutation in a String (hard)

## Phrases for Algorithm Description

1. Use a [*HashMap*] to remember the frequency of each character we have processed
2. First, we will insert characters from the beginning of the string until we have ‘K’ distinct characters in the **HashMap**.
3. These characters will constitute our sliding window. We are asked to find the [*longest*] such window [*having no more than ‘K’ distinct characters*]. We will remember [*the length of this window*] as the [*longest*] window so far.
4. After this, we will keep [*adding one character in the sliding window*] (i.e. slide the window ahead), in a stepwise fashion.
5. In each step, we will try to shrink the window from the beginning if [*the count of distinct characters in the **HashMap** is larger than ‘K’*]. We will shrink the window until [*we have no more than ‘K’ distinct characters in the **HashMap***]. This is needed as we intend to find the [*longest*] window.
6. While shrinking, we’ll decrement the frequency of the character going out of the window and remove it from the **HashMap** if its frequency becomes zero.
7. At the end of each step, we’ll check if the current window [*length is the longest*] so far, and if so, [*remember its length*].

- In the following loop we'll try to extend the range [windowStart, windowEnd]
- The time complexity of the above algorithm will be `O(N)` where `N` is the number of the input string.
- The outer `for` loop runs for all characters and the inner while loop processes each character only once, therefore the time complexity of the algorithm will be `O(N + N)` which is asymptotically equivalent to `O(N)`
- The space complexity of the algorithm is `O(K)`, as we will be storing a maximum of `K+1` characters in the HashMap.
- The algorithm runs in constant space `O(1)` as there can be a maximum of three types of fruits stored in the frequency map.
- Whenever we get a repeating character, we will shrink our sliding window to ensure that we always have distinct cahracters in the sliding window.
- This also means K <= N, because in the worst case, the whole string might not have any repeating character so the entire string will be added to the HashMap.
- Having said that,
- Since we can expect a fixed set of characters in the input string, 
- We can say that the algorithm runs in fixed space `O(1)`
- In this case, we can use a **fixed-size array instead of the HashMap**
- Iterate through the string to add one letter at a time in the window. 
- we'll **keep track of** the count of the maximum repeating letter in any window 
- At any time, we know that we can have a window which has one letter repeating `maxRepeatCount` times.

## Syntax

`map.getOrDefault()`

`map.get()`

`map.remove()`

`map.containsKey()`

## Best Practices

- Better to update maximum as the final step of a `for` loop. 
- Keep track of last appearance index or times of appearances
- Shrink by jumping or moving slowly one step at a time
- Identify if there's a `continuous` requirement on subarray or substring
  - e.g. Cotaining a permutation of string doesn't means the permutation has to be continuous. It's also acceptable to have the characters of pattern string scattered.
- `matchCnt`

### Abstraction

```java
class Window {
    Map<Integer, Integer> count;
    int nonzero;

    Window() {
        count = new HashMap();
        nonzero = 0;
    }

    void add(int x) {
        count.put(x, count.getOrDefault(x, 0) + 1);
        if (count.get(x) == 1)
            nonzero++;
    }

    void remove(int x) {
        count.put(x, count.get(x) - 1);
        if (count.get(x) == 0)
            nonzero--;
    }

    int different() {
        return nonzero;
    }
}
```



## Mistakes

- K distinct characters **!=** No duplicate character
- Remember to shrink the window by `windowStart++`
- Take care how many times you are allowed to flip 0 to 1

- [x] Longest Substring Without Repeating Characters

  - Shoule be able to use HashSet and HashMap

  - `int maxLen = 0;`

  - ```java
    public int lengthOfLongestSubstring(String s) {
        int maxLen = 0;
        int windowStart = 0;
        Set<Character> charSet = new HashSet<>();
        for (int windowEnd = 0; windowEnd < s.length(); windowEnd++) {
            char curr = s.charAt(windowEnd);
            while (charSet.contains(curr) && windowStart <= windowEnd) {
                char charStart = s.charAt(windowStart);
                charSet.remove(charStart);
                windowStart++;
            }
            charSet.add(curr);
            maxLen = Math.max(maxLen, windowEnd - windowStart + 1);
        }
    
        return maxLen;
    }
    ```

    - Time complexity: `O(2n) = O(n)`. In the worst case each character will be visited twice by windowStart and windowEnd.

  - The above solution requires at most 2n steps. In fact, it could be optimized to require only n steps. Instead of using a set to tell if a character exists or not, we could define a mapping of the characters to its index. Then we can skip the characters immediately when we found a repeated character.

- [x] Minimum Window Substring

  - Contain all characters => including duplicates

- [x] Sliding Window Maximum

  - ```ArrayDeque<Integer> deque = new ArrayDeque<Integer>();```
  - Let's use a *deque* (double-ended queue), the structure which pops from / pushes to either side with the same `O(1) `performance.
  - It's more handy to store in the deque **indexes instead of elements** since both are used during an array parsing.

- [x] Longest Substring with At Most K Distinct Characters

  - Forgot to update `windowStart`

- [x] Longest Repeating Character Replacement

  - ```if(k > s.length() || s.length() == 0) return s.length();```

- [x] Permutation in String

  - substring should be continuous

- [x] Longest Turbulent Subarray

  - Turbulent => strict larger or smaller => carefully consider the equal case

  - Take care of corner situation: A.length <= 2

  - Better approach: These alternating comparisons form contiguous blocks. We know when the next block ends: when it is the last two elements being compared, or when the sequence isn't alternating.

  - ```java
    public int maxTurbulenceSize(int[] A) {
        int N = A.length;
        int maxLen = 1;
        int windowStart = 0;
        for (int i = 1; i < N; i++) {
            // Integer.compare()
            int c = Integer.compare(A[i-1], A[i]);
            if (c == 0) { 
                // Read the definition of turbulent carefully
                windowStart = i;
            } else if (i == N - 1 || c * Integer.compare(A[i], A[i+1]) != -1) {
                // Always make sure relevant variables are updated
                maxLen = Math.max(maxLen, i - windowStart + 1);
                windowStart = i;
            }
        }
    
        return maxLen;
    }
    ```

- [x] Subarrays with K Different Integers

  - The intuition is that after adding an extra element to our array, it is already valid or we need to shrink them a little bit to keep it valid.
  - When a valid subarray is found, its subarrays with larger left end point and the same right end point might also be valid.
  - We can keep two windows, one for `cnt > K`, one for `cnt >= K`

- [x] **Moving Stones Until Consecutive II**

  - ```java
    public int[] numMovesStonesII(int[] A) {
      Arrays.sort(A);
      int i = 0, n = A.length, low = n;
      int high = Math.max(A[n - 1] - n + 2 - A[1], A[n - 2] - A[0] - n + 2);
      for (int j = 0; j < n; ++j) {
      	while (A[j] - A[i] >= n) ++i;
        if (j - i + 1 == n - 1 && A[j] - A[i] == n - 2)
          low	 = Math.min(low, 2);
        else
          low = Math.min(low, n - (j - i + 1));
      }
      return new int[] {low, high};
    }
    ```

  - If don't sort at the beginning, we will have to use nested `for-loop`. It's also not convinient to count missing stones. So sorting is necessary for this question.

  - Lower Bound: in case of `n` stones, we need to find a consecutive `n` positions and move the stones in.This idea led the solution with sliding windows. Slide a window of size `N`, and find how many stones are already in this window. We want to move other stones into this window. For each missing stone, we need at least one move. Generally, the number of missing stones and the moves we need are the same. **Only one corner case in this problem, we need to move the endpoint to no endpoint.**

  - Upper Bound: We try to move all stones to leftmost or rightmost. For example of to rightmost.
    We move the `A[0]` to `A[1] + 1`. Then each time, we pick the stone of left endpoint, move it to the next empty position. During this process, the position of leftmost stones increment 1 by 1 each time. Until the leftmost is at `A[n - 1] - n + 1`.

- [x]  Minimum Swaps to Group All 1's Together
  - take care of corner case when `oneCnt = 0`

- [x] [Get Equal Substrings Within Budget](https://leetcode.com/problems/get-equal-substrings-within-budget)  
- [ ] 