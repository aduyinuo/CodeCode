## Challenges

- [x] Tree Diameter
- [x] **Path with maximum sum**

- [ ] 

## Phrases for Algorithm Description

- To recursively traverse a binary tree in a DFS fashion, we can start from the root and at every step, make two recursive calls, one for the left and one for the right child.
- DFS:
  - Start DFS with the root of the tree.
  - If the current node is not a leaf node, do two things:
    - Subtract the value of current node from the given number to get a new sum
    - Make two recursive calls for both the children of the current node with the new number calculated in the previous step.
  - At every step, see if the current node being visited is a leaf node and if its value is equal to the given number `S`. If both conditions are true, we have found the required root-to-leaf path, therefore return `true`.
  - If the current not is a leaf but its value is not equal to the given number `S`, return false.
- The space complexity of DFS will be `O(N)` in the worst case. This space will be used to store the recursion stack. The worst case will happen when the given tree is a linked list (i.e., every node has only one child).
- Every time we find a valid root-to-leaf path, we will store it in a list.
- The time complexity of the above algorithm is `O(N^2)`, where `N` is the total number of nodes in the tree. This is due to the fact that we traverse each node once (which will take `O(N)`), and for each leaf node we might have to store its path which will take `O(N)`.
- We can follow DFS approach and additionally, track the element of the given sequence that we should match with the current node. Also, we can return false as soon as we find a mismatch between the sequence and the node value.
- Count Paths
  - We will keep track of the current path in a list which will be passed to every recursive call.
  - Whenever we traverse a node we will do two things:
    - Add the current node to the current path.
    - As we added a new node to the current path, we should find the sums of all sub-paths ending at the current node. If the sum of any sub-path is equal to target, we will increment our path count.
  - We will traverse all paths and will not stop processing after finding the first path
  - Remove the current node from the current path before returning from the function. This is needed to **Backtrack** while we are going up the recursive call stack to process other paths.
- Diameter
  - At every step, we need to find the height of both children of the current node. For this, we will make two recursive calls similar to **DFS**
  - The height of the current node will be equal to the height of the left child or right child + 1
  - To find the overall tree diameter, we will use a class level variable. This variable will store the maximum diameter of all the nodes visited so far, hence, eventually, it will have the final tree diameter.
- Ignore paths with negative sums

## Syntax

```java
ListIterator<Integer> pathIterator = currentPath.listIterator(currentPath.size());
while (pathIterator.hasPrevious())
currentPath.remove(currentPath.size() - 1);
```



## Best Practices

- ```java
  if (currentNode == null)
    return;
  if (currentNode.val == sum && currentNode.left == null && currentNode.right == null) {
  } 
  ```

- Make it clear if the required path is *root-to-leaf* path or is allowed to start and end at any node, and if it should follow direction from parent to child (top to bottom).

## Mistakes

- ```java
  if (sequenceIndex >= sequence.length || currentNode.val != sequence[sequenceIndex])
    return false;
  ```

  - Either the sequence or the path can be longer, and both cases are invalid.

## Abstraction

- 

