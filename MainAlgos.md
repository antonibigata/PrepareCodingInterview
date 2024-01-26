# Vanilla Binary Search

## Overview

Binary search is an efficient algorithm for finding an item from a sorted list of items. It works by repeatedly dividing in half the portion of the list that could contain the item, until you've narrowed down the possible locations to just one.

## Basic Algorithm

The basic steps of binary search are:

1. **Initialize**: Start with two pointers, `low = 0` and `high = length of array - 1`.
2. **Loop**: While `low` <= `high`:
   - Find the middle element `mid = low + (high - low) / 2`.
   - If the middle element is equal to the target, return `mid`.
   - If the target is less than the middle element, move the `high` pointer to `mid - 1`.
   - If the target is greater than the middle element, move the `low` pointer to `mid + 1`.
3. **Result**: If the target is not found, return `-1`.

## Complexity

- Time Complexity: O(log n), where n is the number of elements in the array.
- Space Complexity: O(1) for iterative implementation.

## Variations

Binary search can be adapted for various scenarios, such as:
- Finding the first or last occurrence of a value in a sorted array.
- Finding the closest value to a target.
- Searching in a rotated sorted array.

## Implementation

Example in Python:

```python
def binary_search(arr, target):
    low, high = 0, len(arr) - 1
    while low <= high:
        mid = low + (high - low) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            low = mid + 1
        else:
            high = mid - 1
    return -1
```

## Tips for Interviews

- Ensure the array is sorted before using binary search.
- Consider edge cases, such as empty arrays or arrays with duplicate values.
- Clearly explain the reasoning behind adjusting the `low` and `high` pointers.

# BFS Fundamentals

## Overview
Breadth-First Search (BFS) is a fundamental algorithm for traversing or searching tree and graph data structures. It explores all nodes at the present depth level before moving on to the nodes at the next depth level.

## Basic Algorithm
The algorithm uses a queue data structure to track which vertex to visit next. Upon visiting a node, all of its adjacent nodes are discovered and added to the queue.

1. **Initialization**: 
   - Start with a queue and add the root node (or starting node in a graph).
   - Mark the starting node as visited.

2. **Traversal**:
   - While the queue is not empty:
     - Dequeue a node from the queue and process it.
     - Iterate over all adjacent nodes.
     - For each adjacent node, if it has not been visited, mark it as visited and enqueue it.

3. **Completion**:
   - The algorithm completes when the queue becomes empty, meaning all reachable nodes have been visited.

## Complexity
- Time Complexity: O(V + E), where V is the number of vertices and E is the number of edges.
- Space Complexity: O(V), due to the storage needed for the visited set and queue.

## Applications
- Finding the shortest path on unweighted graphs.
- Level order traversal of trees.
- Algorithms that require visiting each vertex of a graph in an order closest to the starting point.

## Implementation Example (Python)
```python
from collections import deque

def bfs(graph, start):
    visited, queue = set(), deque([start])
    visited.add(start)
    while queue:
        vertex = queue.popleft()
        print(str(vertex) + " ", end="")
        # Add all unvisited neighbors to the queue
        for neighbour in graph[vertex]:
            if neighbour not in visited:
                visited.add(neighbour)
                queue.append(neighbour)
```

## Tips for Interviews
- Understand the difference between DFS and BFS.
- Consider edge cases such as disconnected graphs and cycles.
- Be able to implement BFS both iteratively and recursively (if applicable).


# DFS Fundamentals

## Overview
Depth-First Search (DFS) is a fundamental algorithm used in graph theory for traversing or searching through the nodes of a graph. It explores as deep as possible along each branch before backtracking.

## Basic Algorithm
DFS can be implemented using recursion or a stack. The basic idea is to start from a node, mark it as visited, and recursively visit its adjacent (and unvisited) nodes.

1. **Start at a Node**: Choose a starting node.
2. **Mark as Visited**: Mark this node as visited.
3. **Recursive Exploration**: For each unvisited neighbor of the current node, call DFS on that neighbor.
4. **Backtrack**: Continue until all nodes are visited or the node has no unvisited neighbors.

## Applications
- Pathfinding and checking for connectivity in graphs.
- Topological sorting in directed graphs.
- Finding strongly connected components in a graph.

## Complexity
- Time Complexity: O(V + E), where V is the number of vertices and E is the number of edges.
- Space Complexity: O(V), mainly due to the recursion stack.

## Implementation Example (Python)
```python
def dfs(graph, node, visited):
    if node not in visited:
        print(node, end=" ")
        visited.add(node)
        for neighbour in graph[node]:
            dfs(graph, neighbour, visited)
```

## Tips for Interviews
- Understand when to use DFS vs. BFS.
- Be familiar with both recursive and iterative implementations of DFS.
- Consider edge cases, such as disconnected graphs and graphs with cycles.

# Heap Fundamentals

## Overview
A heap is a specialized tree-based data structure that satisfies the heap property. It can be classified mainly into two types: max-heaps and min-heaps.

- **Max-Heap**: In a max-heap, for any given node `i`, the value of `i` is greater than or equal to the values of its children.
- **Min-Heap**: In a min-heap, for any given node `i`, the value of `i` is less than or equal to the values of its children.

## Heap Operations
Common operations performed on heaps include:

1. **Insertion**:
   - Add a new element to the end of the heap.
   - "Heapify up" the new element, swapping it with its parent until the heap property is restored.

2. **Extraction**:
   - Remove the root element (max in max-heap or min in min-heaps).
   - Replace the root with the last element in the heap.
   - "Heapify down" the new root, swapping it with its largest (or smallest for min-heaps) child until the heap property is restored.

3. **Peek**:
   - Return the root element without removing it from the heap.

4. **Heapify**:
   - Convert an unsorted array into a heap by performing "heapify down" operations starting from the last non-leaf node to the root.

## Complexity
- Insertion: O(log n)
- Extraction: O(log n)
- Peek: O(1)
- Heapify: O(n)

## Implementation
Heaps are often implemented using arrays for efficiency. The children of the node at index `i` are at indices `2i + 1` and `2i + 2`, and its parent is at index `(i - 1) / 2`.

## Applications
- Implementing priority queues.
- Efficiently finding the kth largest (or smallest) element in an array.
- Dijkstra's and Prim's algorithms.

## Example (Python)
Example of a min-heap implementation:
```python
import heapq

# Create a min-heap
min_heap = []
heapq.heappush(min_heap, 5)
heapq.heappush(min_heap, 3)
heapq.heappush(min_heap, 7)

# Extract the minimum element
min_value = heapq.heappop(min_heap)
```

## Tips for Interviews
- Understand how to implement heaps and perform heap operations.
- Know when to use a heap vs. other data structures like sorted arrays or BSTs.
- Be familiar with heap applications, especially in problems involving priority queues or sorting.

# Keyword to Algorithm

### "Top k"

-   Heap: [K closest points](https://algo.monster/problems/k_closest_points)

### "How many ways.."

-   DFS: [Decode ways](https://algo.monster/problems/decode_ways)
-   DP: [Robot paths](https://algo.monster/problems/robot_unique_path)

### "Substring"

-   Sliding window: [Longest substring without repeating characters](https://algo.monster/problems/longest_substring_without_repeating_characters)

### "Palindrome"

-   two pointers: [Valid Palindrome](https://algo.monster/problems/valid_palindrome)
-   DFS: [Palindrome Partitioning](https://algo.monster/problems/palindrome_partitioning)
-   DP: [Palindrome Partitioning 2](https://algo.monster/problems/palindrome_partitioning_2)

### "Tree"

-   shortest, level-order
    -   BFS: [Binary tree level-order traversal](https://algo.monster/problems/binary_tree_level_order_traversal)
-   else: DFS: [Max Depth](https://algo.monster/problems/tree_max_depth)

### "Parentheses"

-   Stack: [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

### "Subarray"

-   Sliding window: [Maximum subarray sum](https://algo.monster/problems/subarray_sum_fixed)
-   Prefix sum: [Subarray sum](https://algo.monster/problems/subarray_sum)
-   Hashmap: [Continuous subarray sum](https://leetcode.com/problems/continuous-subarray-sum/)

### Max subarray

-   Greedy: [Kadane's Algorithm](https://en.wikipedia.org/wiki/Maximum_subarray_problem#Kadane's_algorithm)

### "X Sum"

-   Two pointer: [Two sum](https://algo.monster/problems/two_sum_sorted)

### "Max/longest sequence"

-   Dynamic programming, DFS: [Longest increasing subsequence](https://algo.monster/problems/longest_increasing_subsequence)
-   mono deque: [Sliding window maximum](https://algo.monster/problems/sliding_window_maximum)

### "Minimum/Shortest"

-   Dynamic programming, DFS: [Minimal path sum](https://algo.monster/problems/minimal_path_sum)
-   BFS: [Shortest path](https://algo.monster/problems/shortest_path_unweight)

### "Partition/split ... array/string"

-   DFS: [Decode ways](https://algo.monster/problems/decode_ways)

### "Subsequence"

-   Dynamic programming, DFS: [Longest increasing subsequence](https://algo.monster/problems/longest_increasing_subsequence)
-   Sliding window: [Longest increasing subsequence](https://algo.monster/problems/longest_increasing_subsequence)

### "Matrix"

-   BFS, DFS: [Flood fill](https://algo.monster/problems/flood_fill), [Islands](https://algo.monster/problems/number_of_islands)
-   Dynamic programming: [Maximal square](https://algo.monster/problems/maximal_square)

### "Jump"

-   Greedy/DP: [Jump game](https://leetcode.com/problems/jump-game/)

### "Game"

-   Dynamic programming: [Divisor game](https://algo.monster/problems/divisor_game), [Stone game](https://algo.monster/problems/divisor_game)

### "Connected component", "Cut/remove" "Regions/groups/connections"

-   Union Find: [Number of connected components](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/), [Redundant connections](https://leetcode.com/problems/redundant-connection/)

### Transitive relationship

If the items are related to one another and the relationship is transitive, then chances are we can build a graph and use BFS or Union Find.

-   string converting to another, BFS: [Word Ladder](https://algo.monster/problems/word_ladder)
-   string converting to another, BFS, Union Find: [Sentence Similarity](https://leetcode.com/problems/sentence-similarity-ii/)
-   numbers having divisional relationship, BFS, Union Find: [Evaluate Division](https://leetcode.com/problems/evaluate-division/)
