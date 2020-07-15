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



## Mistakes

- K distinct characters **!=** No duplicate character
- Remember to shrink the window by `windowStart++`
- Take care how many times you are allowed to flip 0 to 1

