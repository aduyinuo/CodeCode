## Challenges

- [x] Minimum Meeting Rooms
- [x] Maximum CPU Load
- [x] Employee Free Time

## Phrases for Algorithm Description

- The space complexity of the above algorithm will be `O(N)` as we need to return a list containing all the merged intervals. 
- We will also need `O(N)` **space for sorting**. √√√
- If the given list was not sorted, we could have simply appended the new interval to it and used the `merge()` function. But since the given list is sorted, we should try to come up with a solution better that `O(nLogN)` 
- Our algorithm will be to iterate through both the lists together to see if any two intervals overlap. **If two intervals overlap, we will insert the overlapped part into a result list and move on to the next interval which is finishing early**.
- Need: keep track of the ending time of all the meetings currently happening 
- => A Min Heap would fit our requirement best
  - Before scheduling `m1`, remove all meetings from the heap that have ended before m1
  - Add `m1` to the heap
  - Keep a counter to remember the maximum size of the heap at any time which will be the minimum number of rooms needed.
- Keep a **running count** of the maximum CPU load at any time to find the overall maximum load.
- Utilize the fact that each employee list is individually sorted

## Syntax

```java
Collections.sort(intervals, (a, b) -> Integer.compare(a.start, b.start));
Iterator<Interval> intervalItr = intervals.iterator();
Interval interval = intervalItr.next();
while (intervalItr.hasNext()) {
  interval = intervalItr.next();
}
```

```java
if (intervals == null || intervals.isEmpty())
      return Arrays.asList(newInterval);
```

```java
List<Interval> intervalsIntersection = new ArrayList<Interval>();
    return intervalsIntersection.toArray(new Interval[intervalsIntersection.size()]);
```

```java
PriorityQueue<Meeting> minHeap = 
        new PriorityQueue<>(meetings.size(), (a, b) -> Integer.compare(a.end, b.end));
minHeap.isEmpty();
minHeap.peek();
minHeap.poll();
minHeap.offer();
```



## Best Practices

- Sort the intervals on the start time to ensure `a.start <= b.start`

## Mistakes

- 

## Abstraction

- 

