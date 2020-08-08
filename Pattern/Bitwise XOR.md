## Challenges

- [x] Find the Corrupt Pair

## Phrases for Algorithm Description

- Remember the important property of XOR that it returns 0 if both the bits in comparison are the same. In other words, XOR of a number with itself will always result in 0. This means that if we XOR all the numbers in the input array with all numbers from the range 1 to n then each number in the input is going to get zeroed out except the missing number. 
  - XOR all the numbers from 1 to n => x1
  - XOR all the numbers in the input array => x2
  - The missing number can be found by x1 XOR x2
- We can take any bit which is '1' in n1 ^ n2 and partition all numbers in the given array into two groups based on that bit.

## Syntax

```java
new int[] { num1, num2 };
```



## Best Practices

- ```java
  public static int bitwiseComplement(int num) {
    // count number of total bits in 'num'
    int bitCount = 0;
    int n = num;
    while (n > 0) {
      bitCount++;
      n = n >> 1;
    }
  
    // for a number which is a complete power of '2' i.e., it can be written as pow(2, n), if we
    // subtract '1' from such a number, we get a number which has 'n' least significant bits set to '1'.
    // For example, '4' which is a complete power of '2', and '3' (which is one less than 4) has a binary 
    // representation of '11' i.e., it has '2' least significant bits set to '1' 
    int all_bits_set = (int) Math.pow(2, bitCount) - 1;
  
    // from the solution description: complement = number ^ all_bits_set
    return num ^ all_bits_set;
  ```

- Try to complete tasks with one traverse

## Mistakes

- 

## Abstraction

- 

