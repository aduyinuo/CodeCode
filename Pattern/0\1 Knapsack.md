## Challenges

- [x] Count of Subset Sum
- [x] Target Sum


## Phrases for Algorithm Description

- Memoization is when we store the results of all the previously solved sub-problems and return the results from memory if we encounter a problem that has already been solved.
- Since we have two **changing values** (`capacity` and `currentIndex`) in our recursive function, we can use a two-dimensional array to store the results of all the solved sub-problems.
- As we know, the final profit is at the bottom-right corner. Therefore, we will start from there to find the items that will be going into the knapsack.
  - Item skipped => value from the cell right above it
  - item included => value from the cell in same row with `- weight` capacity
- Since our inner loop is iterating over `c: 0-->capacity`, let's see how this might affect our two required values:
  - When we access `dp[c]`, it has not been overridden yet for the current iteration, so it should be fine.
  - `dp[c-weight[i]]` might be overriden if `weight[i]>0`. Therefore we can't use this value for the current iteration.
    - To solve this case, we can change our inner loop to process in the reverse direction: `c:capacity-->0`. This will ensure that whenever we change a value in `dp[]`, we will not need it again in the current iteration.
- Let's assume S1 and S2 are the two desired subsets. A basic brute-force solution could be to try adding each element either in S1 or S2 in order to find the combination that gives the minimum sum difference between the two sets.
- We can use memoization to overcome the overlapping sub-problems.
- We will be using a two-dimensional array to store the results of the solved sub-problems. We can uniquely identify a sub-problem from `currentIndex` and `S1` as `S2` will always be the sum of the remaining numbers.

## Syntax

```java
dp[0][s] = (num[0] == s ? 1 : 0);
```

## Best Practices

- ```java
  // base checks
  
  // recursive call after choosing the element at the currentIndex
  // if the weight of the element at currentIndex exceeds the capacity, we shouldn't process this
  
  // recursive call after excluding the element at the currentIndex
  ```

- ```java
  // base checks
  
  // populate the capacity=0 columns, with 0 capacity we have 0 profit
  
  // if we have only one weight, we will take it if it is not more than the capacity
  
  // process all sub-arrays for all the capacities
  		// include the item, if it is not more than the capacity
  		// exclude the item
  		// take maximum
  
  // maximum profit will be at the bottom-right corner
  ```

- ```java
  // base checks
  if (sum == 0)
    return 1;
  
  if(num.length == 0 || currentIndex >= num.length)
    return 0;
  ```

- 

## Mistakes

- ```java
  
  ```

  - 

- 

## Abstraction

- 
- 

