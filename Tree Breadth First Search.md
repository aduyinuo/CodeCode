## Challenges

- [x] Connect all level order siblings
- [ ] Right View of a Binary Tree

## Phrases for Algorithm Description

- Use a queue to keep track of all the nodes of a level before we jump onto the next level.
- This also means that the space complexity of the algorithm will be `O(W)`, where `W` is the maximum number of nodes on any level. Since we can have a maximum of `N/2` nodes at any level (this could happen only at the lowest level), therefore we will need `O(N)` space to store them in the queue.
- BFS:
  - Start by pushing the root node to the queue.
  - Keep iterating untill the queue is empty.
  - In each iteration, first count the elements in the queue (`levelSize`). We will have these many nodes in the current level.
  - Next, remove `levelSize` nodes from the queue and push their value in an array to represent the current level.
  - After removing each node from the queue, insert both of its children into the queue.
  - If the queue is not empty, repeat from step 3 for the next level.
- The time complexity of **BFS** is `o(N)`, where `N` is the total number of nodes. This is due to the fact that we traverse each node once.
- Alternate traverse direction for each level:
  - Use a boolean to serve as the flag of traverse direction
  - Add the node to the current level based on the traverse direction
- Minimum depth
  - Follow **BFS** approach, track the depth of the tree.
  - As soon as we find our first leaf node, that level will represent the minimum depth of the tree.
- The level order successor is the node that appears right after the given node in the level order traversal
  - As soon as we find the given node, we will return the next node from the queue as the level order successor.
  - What if it's the last node in the tree?
- Connect level order siblings, the last node of each level should point to a `null` node.
- The only additional thing we will be do is to append the last node of each level to the result array.

## Syntax

```java
List<List<Integer>> result = new ArrayList<List<Integer>>();
Queue<TreeNode> queue = new LinkedList<>();
queue.offer(root);
queue.isEmpty();
queue.size();
queue.poll();
List<Integer> currentLevel = new ArrayList<>(levelSize); // size argument
```

```java
if (i == levelSize - 1)
  result.add(currentNode);
```



## Best Practices

- ```java
  TreeNode previousNode = null;
  if (previousNode != null)
    previousNode.next = currentNode;
  previousNode = currentNode;
  ```

- Stick to the pattern as much as possible. Otherwise it would be both error prone and lack of consistency.

## Mistakes

- 

## Abstraction

- 

