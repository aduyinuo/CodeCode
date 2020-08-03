## Challenges

- [x] Evaluate Expression
- [x] Structurally Unique Binary Search Trees
- [x] Count of Structurally Unique Binary Search Trees

## Phrases for Algorithm Description

- Subsets——BFS
  - Start with an empty set, iterate through all numbers one-by-one, and add them to existing sets to create new subsets.
  - Take all existing subsets and insert the current number in them to create new subsets.
  - Create a new subset from the existing subset and insert the current element to it
- Since, in each step, the number of subsets doubles as we add each element to all the existing subsets, the time complexity is `O(2^N)`. This also means that, in the end, we will have a total of `O(2^N)` subsets.
- Sort the numbers of the given set. This will ensure that all duplicate numbers are next to each other.
- Follow the same BFS approach but whenever we are about to process a duplicate (i.e., when the current and the previous numbers are the same), instead of adding the current number to all the existing subsets, only add it to the subsets which were created in the previous step.
- Following a BFS approach, we will abbreviate one character at a time. At each time we have two options:
  - Continue abbreviating by incrementing the current abbreviation count
  - Restart abbreviating, append the count and the current character to the string
- Evaluate Expression
  - From the perspective of operators
  - Iterate through the expression character-by-character
  - Break the expression into two halves whenever we get an operator
  - The two parts can be calculated by recursively calling the function.
  - Once we have the evaluation results from the left and right halves, we can combine them to produce all results。
  - The problem has overlapping subproblems, as our recursive calls can be evaluating the same sub-expression multiple times. To resolve this, we can use memoization and store the intermediate results in a HashMap. In each function call, we can check our map to see if we have already evaluated this sub-expression before.
- Iterate from 1 to n and consider each number as the root of a tree.

## Syntax

```java
for (int currentNumber : nums)
List<Integer> set = new ArrayList<>(subsets.get(i));
```

## Best Practices

- Use startIndex and endIndex as `timestamp` and differentiate subsets added in previous step. => BFS 
  
- 

## Mistakes

- 

## Abstraction

- Step
  - One character at a time
  - One number at a time
- Level
  - process everything derived previously
  - only process items derived in last step
- Options
  - keep abbreviation or append original character
  - all possible positions in a string0

