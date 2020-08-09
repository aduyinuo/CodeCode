## Challenges

- [ ] 


## Phrases for Algorithm Description

- To find the topological sort of a graph we can traverse the graph in a Breadth First Search (BFS) way. We will start with all the sources, and in a stepwise fashion, save all sources to a sorted list. We will then remove all sources and their edges from the graph. After the removal of the edges, we will have new sources, so we will repeat the above process untill all vertices are visited.

## Syntax

```java

```

## Best Practices

- ```java
  if (sortedOrder.size() != vertices) // topological sort is not possible as the graph has a cycle
    return new ArrayList<>();
  ```

- 

## Mistakes

- ```java
  
  ```

  - 

- 

## Abstraction

- Find a linear ordering of elements that have dependencies on each other
- Source: Any node that has no incoming edge and has only outgoing edges is called a source.
- Sink: Any node that has only incoming edges and no outgoign edges is called a sink.
- So, we can say that a topological ordering starts with one of the sources and ends at one of the sinks.

