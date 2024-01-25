# crackthecodingRECAP


# Big O

  

Certainly! Let's dive deeper into each common Big O notation case to provide a clearer understanding:

  

### 1. O(1) - Constant Time

In an O(1) algorithm, the time taken to execute is constant and does not depend on the size of the input. This means that no matter how large your input is, the algorithm will take the same amount of time to complete.

  

**Example**: Accessing an element in an array by index.

- Regardless of the array's size, accessing an element at a specific index takes the same amount of time.

  

### 2. O(log n) - Logarithmic Time

An algorithm is O(log n) when its runtime increases logarithmically in proportion to the input size. These algorithms typically reduce the problem size by half each step, making them much more efficient than linear algorithms for large inputs.

  

**Example**: Binary Search.

- Binary search splits the data in half each time, reducing the problem size significantly with each step. Thus, for a list of size `n`, it only takes `log2(n)` steps to find the element or conclude it's not present.

  

### 3. O(n) - Linear Time

An O(n) algorithm's execution time increases linearly with the input size. This means the time taken grows directly in proportion to the number of elements in the input.

  

**Example**: Finding the maximum element in an array.

- You need to look at each element in the array to determine the maximum, so the time taken grows with the array's size.

  

### 4. O(n log n)

This is often seen in efficient sorting algorithms. The O(n log n) complexity arises when the algorithm performs a logarithmic number of operations (like comparisons or merges) n times.

  

**Example**: Merge Sort.

- Merge sort recursively divides the array into halves and then merges the sorted halves. The division is logarithmic (O(log n)), and the merge operation is linear (O(n)), combining to O(n log n).

  

### 5. O(n^2) - Quadratic Time

In an O(n^2) algorithm, the execution time is proportional to the square of the input size. This is common in algorithms that have nested iterations over the data.

  

**Example**: Bubble Sort.

- For each element, bubble sort compares it with every other element, leading to n*(n-1)/2 comparisons, which simplifies to O(n^2).

  

### 6. O(2^n) - Exponential Time

These algorithms have runtimes that double with each additional input element. They are often recursive algorithms where each function call branches into two more calls.

  

**Example**: Fibonacci sequence (naive recursive approach).

- Each call to `fibonacci(n)` results in two more calls: `fibonacci(n-1)` and `fibonacci(n-2)`. This causes an exponential growth in the number of calls.

  

### Understanding the Implications

- **Scalability**: As input size increases, algorithms with lower Big O complexities scale better.

- **Trade-offs**: Sometimes a higher complexity algorithm might be more suitable due to factors like easier implementation or better average-case performance.

- **Optimization**: Understanding Big O helps in optimizing algorithms for performance-critical applications.

  

In interviews, demonstrating an understanding of these concepts and being able to apply them to real problems is key. Practice analyzing algorithms' complexities and think about how they perform with various input sizes.

  

# Lookup/access


# Time Complexity - Python Wiki

This page documents the time-complexity (aka "Big O" or "Big Oh") of various operations in current CPython. Other Python implementations (or older or still-under development versions of CPython) may have slightly different performance characteristics. However, it is generally safe to assume that they are not slower by more than a factor of O(log n). 

Generally, 'n' is the number of elements currently in the container. 'k' is either the value of a parameter or the number of elements in the parameter. 

## list

The Average Case assumes parameters generated uniformly at random. 

Internally, a list is represented as an array; the largest costs come from growing beyond the current allocation size (because everything must move), or from inserting or deleting somewhere near the beginning (because everything after that must move). If you need to add/remove at both ends, consider using a `collections.deque` instead. 

| Operation          | Average Case | Amortized Worst Case |
|--------------------|--------------|----------------------|
| Copy               | O(n)         | O(n)                 |
| Append[1]          | O(1)         | O(1)                 |
| Pop last           | O(1)         | O(1)                 |
| Pop intermediate[2]| O(n)         | O(n)                 |
| Insert             | O(n)         | O(n)                 |
| Get Item           | O(1)         | O(1)                 |
| Set Item           | O(1)         | O(1)                 |
| Delete Item        | O(n)         | O(n)                 |
| Iteration          | O(n)         | O(n)                 |
| Get Slice          | O(k)         | O(k)                 |
| Del Slice          | O(n)         | O(n)                 |
| Set Slice          | O(k+n)       | O(k+n)               |
| Extend[1]          | O(k)         | O(k)                 |
| Sort               | O(n log n)   | O(n log n)           |
| Multiply           | O(nk)        | O(nk)                |
| x in s             | O(n)         |                      |
| min(s), max(s)     | O(n)         |                      |
| Get Length         | O(1)         | O(1)                 |

## collections.deque

A deque (double-ended queue) is represented internally as a doubly linked list. (Well, a list of arrays rather than objects, for greater efficiency.) Both ends are accessible, but even looking at the middle is slow, and adding to or removing from the middle is slower still. 

| Operation   | Average Case | Amortized Worst Case |
|-------------|--------------|----------------------|
| Copy        | O(n)         | O(n)                 |
| append      | O(1)         | O(1)                 |
| appendleft  | O(1)         | O(1)                 |
| pop         | O(1)         | O(1)                 |
| popleft     | O(1)         | O(1)                 |
| extend      | O(k)         | O(k)                 |
| extendleft  | O(k)         | O(k)                 |
| rotate      | O(k)         | O(k)                 |
| remove      | O(n)         | O(n)                 |
| Get Length  | O(1)         | O(1)                 |

## set

See dict -- the implementation is intentionally very similar. 

| Operation                           | Average case              | Worst Case                |
|-------------------------------------|---------------------------|---------------------------|
| x in s                              | O(1)                      | O(n)                      |
| Union s\|t                          | O(len(s)+len(t))          |                           |
| Intersection s&t                    | O(min(len(s), len(t)))    | O(len(s) * len(t))        |
| Multiple intersection s1&s2&..&sn   | (n-1)*O(l) where l is max(len(s1),..,len(sn)) |
| Difference s-t                      | O(len(s))                 |                           |
| s.difference_update(t)              | O(len(t))                 |                           |
| Symmetric Difference s^t            | O(len(s))                 | O(len(s) * len(t))        |
| s.symmetric_difference_update(t)    | O(len(t))                 | O(len(t) * len(s))        |

## dict

The Average Case times listed for dict objects assume that the hash function for the objects is sufficiently robust to make collisions uncommon. The Average Case assumes the keys used in parameters are selected uniformly at random from the set of all keys. 

Note that there is a fast-path for dicts that (in practice) only deal with str keys; this doesn't affect the algorithmic complexity, but it can significantly affect the constant factors: how quickly a typical program finishes. 

| Operation    | Average Case | Amortized Worst Case |
|--------------|--------------|----------------------|
| k in d       | O(1)         | O(n)                 |
| Copy[3]      | O(n)         | O(n)                 |
| Get Item     | O(1)         | O(n)                 |
| Set Item[1]  | O(1)         | O(n)                 |
| Delete Item  | O(1)         | O(n)                 |
| Iteration[3] | O(n)         | O(n)                 |

### Notes
[1] These operations rely on the "Amortized" part of "Amortized Worst Case". Individual actions may take surprisingly long, depending on the history of the container. 

[2] Popping the intermediate element at index k from a list of size n shifts all elements after k by one slot to the left using memmove. n - k elements have to be moved, so the operation is O(n - k). The best case is popping the second to last element, which necessitates one move, the worst case is popping the first element, which involves n - 1 moves. The average case for an average value of k is popping the element the middle of the list, which takes O(n/2) = O(n) operations. 

[3] For these operations, the worst case n is the maximum size the container ever achieved, rather than just the current size. For example, if N objects are added to a dictionary, then N-1 are deleted, the dictionary will still be sized for N objects (at least) until another insertion is made. 

  
 # Trees and Graphs

  

Certainly! Trees and graphs are fundamental data structures often discussed in coding interviews. Understanding these structures and their associated algorithms is crucial for solving many problems in computer science.

  

### Trees

A tree is a hierarchical data structure consisting of nodes connected by edges. It has the following properties:

- **Root**: The top node without a parent.

- **Children**: Nodes linked to a parent node.

- **Leaf Nodes**: Nodes without children.

- **Height**: Length of the longest path from the root to a leaf.

- **Depth**: The distance from the root to a node.

  

**Common Types of Trees**:

1. **Binary Tree**: Each node has at most two children, typically referred to as the left and right child.

2. **Binary Search Tree (BST)**: A binary tree where for each node, all elements in the left subtree are less than the node, and all elements in the right subtree are greater.

3. **Balanced Trees** (e.g., AVL trees, Red-Black trees): BSTs where the height is kept balanced to ensure O(log n) time complexity for insertions, deletions, and lookups.

4. **Heap**: A special tree-based data structure where the tree is a complete binary tree, and each node follows a specific order (e.g., max-heap, min-heap).

  

**Tree Traversal Algorithms**:

1. **In-Order Traversal**: Left subtree, root, right subtree (commonly used in BSTs to get sorted order).

2. **Pre-Order Traversal**: Root, left subtree, right subtree.

3. **Post-Order Traversal**: Left subtree, right subtree, root.

4. **Level-Order Traversal** (Breadth-First Search): Traverses the tree level by level.

  

### Graphs

A graph is a collection of nodes (vertices) connected by edges. Graphs can model various real-world problems, such as networks, relationships, and paths.

  

**Properties**:

- **Directed vs. Undirected**: Directed graphs have directed edges (arrows), whereas undirected graphs have undirected edges.

- **Weighted vs. Unweighted**: Edges in weighted graphs have values (weights) associated with them, representing cost, length, etc.

- **Cyclic vs. Acyclic**: Cyclic graphs contain cycles, while acyclic graphs do not.

  

**Graph Representation**:

1. **Adjacency Matrix**: A 2D array where the element at `matrix[i][j]` indicates whether there is an edge from node `i` to node `j`.

2. **Adjacency List**: A list where each element represents a node, and stores a list of nodes that it is connected to.

  

**Graph Algorithms**:

1. **Depth-First Search (DFS)**: Explores as far as possible along each branch before backtracking (can be implemented using recursion or a stack).

2. **Breadth-First Search (BFS)**: Explores all neighbors at the present depth before moving to the nodes at the next depth level (implemented using a queue).

3. **Dijkstra's Algorithm**: Finds the shortest path from a single source node to all other nodes in a weighted graph.

4. **Bellman-Ford Algorithm**: Computes shortest paths from a single source vertex to all other vertices in a weighted graph; it can handle negative weights.

5. **Floyd-Warshall Algorithm**: Finds shortest paths between all pairs of vertices in a weighted graph.

  

### Tips for Interviews

- Understand how to implement and manipulate these structures.

- Practice common algorithms and understand their time and space complexities.

- Be prepared to apply these concepts to solve problems, such as finding the shortest path, detecting cycles, or traversing trees in specific orders.

- Explain your thought process clearly and consider edge cases and optimization opportunities.

  

Trees and graphs are versatile structures used in many algorithmic problems, so having a solid grasp of them is highly beneficial for coding interviews.

  

# BFS/DFS

  

Sure, let's delve into more detail about Depth-First Search (DFS) and Breadth-First Search (BFS), two fundamental graph traversal algorithms, along with examples.

  

### Depth-First Search (DFS)

DFS is a traversal algorithm that explores as far as possible along each branch before backtracking. It's commonly used to explore the entire graph or to search for specific elements, paths, or properties within a graph.

  

**How it works**:

1. Start at a selected node (root if a tree, any node if a graph).

2. Visit the node and mark it as visited.

3. Recursively visit each unvisited adjacent node.

  

DFS can be implemented using recursion or with a stack. The recursive approach is more straightforward and commonly used.

  

**Example**: Consider a binary tree. We want to perform DFS to print each node's value.

  

![](https://lh7-us.googleusercontent.com/02fMLNe8hA_IZJNs5UHxj7ONx_czS9SDOcxmqhJ8i8Xq0TqQbW529WeZVqWJpUgN3hOO7dyRyug9ko8IDHkBhJjnCzdOi61XlFB3ZJ4ZKhhDR62S3qTFf0nXwH5h6voRJNPlxt1b9EaAZhus-TblSBQ)

In this example, the `dfs` function is called recursively to visit and print the value of each node in the tree.

  

### Breadth-First Search (BFS)

BFS is a traversal algorithm that explores all the neighbors at the present depth level before moving on to the nodes at the next depth level. It's used for finding the shortest path on unweighted graphs or for traversing a tree level by level.

  

**How it works**:

1. Start at a selected node.

2. Visit the node and mark it as visited.

3. Add all unvisited adjacent nodes to a queue.

4. Dequeue a node and repeat the process until the queue is empty.

  

BFS is typically implemented using a queue.

  

**Example**: Consider the same binary tree structure. We want to perform BFS to print each node's value.

  

![](https://lh7-us.googleusercontent.com/KZzV2EE6bY1Bg3s-KeqOrAdOoYof0jzIo-wtk1xmfWbaQ7CmROXbI3J911o7Pm8m06EC27az9L1-RDXBJEpB4QIpNwJnTCz53qrvPmach9Qm9ea39ZxUV-FYXVTKpPnkWh-xDNy96FyVpOuRtQAWV_8)

  

In this example, we use a queue to iteratively visit and print the value of each node in the tree, level by level.

  

### Key Differences

- **DFS**:

- Uses a stack (explicit or via recursion).

- Goes as deep as possible in one direction before backtracking.

- More space-efficient on wide trees/graphs.

- Better for scenarios where solutions are likely to be found deep in the tree/graph.

  

- **BFS**:

- Uses a queue.

- Explores neighbors before going deeper.

- More space-efficient on deep trees/graphs.

- Finds the shortest path on unweighted graphs.

  

Both DFS and BFS are essential for various problems in graph theory, and understanding their implementations and use cases is critical for coding interviews.

  

# Bit manipulation

  

Certainly! Bit manipulation is a key topic in computer science and software engineering, especially in the context of technical interviews. It involves working directly with bits, which are the most basic units of data in computing, represented as either 0 or 1. Bit manipulation operations are fast and efficient, making them important for optimizing code, solving certain types of problems, and understanding low-level data processing.

  

### Understanding Bits

- Bits are the basic building blocks in computing.

- Binary numbers are composed of bits (0s and 1s).

  

### Common Bitwise Operators

1. **AND (&)**: Compares two bits and returns 1 if both are 1, otherwise 0.

- Example: `101 & 001` results in `001`.

2. **OR (|)**: Compares two bits and returns 1 if either of the bits is 1.

- Example: `101 | 001` results in `101`.

3. **XOR (^)**: Compares two bits and returns 1 if exactly one of the bits is 1.

- Example: `101 ^ 001` results in `100`.

4. **NOT (~)**: Inverts the bits (0 becomes 1, and 1 becomes 0).

- Example: `~101` results in `010` (inverting each bit).

5. **Left Shift (<<)**: Shifts bits to the left, adding 0s on the right.

- Example: `101 << 2` results in `10100`.

6. **Right Shift (>>)**: Shifts bits to the right. For unsigned types, 0s are added on the left.

- Example: `101 >> 2` results in `001`.

  

### Bit Manipulation Techniques

- **Setting a Bit**: Turn a specific bit to 1.

- `num |= (1 << i)`

- **Clearing a Bit**: Turn a specific bit to 0.

- `num &= ~(1 << i)`

- **Toggling a Bit**: Flip a specific bit.

- `num ^= (1 << i)`

- **Checking a Bit**: Determine if a specific bit is set to 1.

- `(num & (1 << i)) != 0`

  

### Practical Uses in Interviews

- **Memory Efficiency**: Operations on individual bits use less memory.

- **Speed**: Bitwise operations are often faster than arithmetic operations.

- **Problem Solving**: Useful in solving specific problems like bit masks, encoding/decoding data, or optimizing algorithms.

  

### Example Problem: Counting Set Bits

Count the number of 1s in the binary representation of a number.

  

![](https://lh7-us.googleusercontent.com/SIDfAWoO2qFTgEVnToA8m2r5PR-P-LgOiqFuAgbbtGGBfQ6x90hAT4qfWNF59JIc-Ef0GlKu8l0kGnCTJ6NYHtA-8DkJ-64hJqrP9W1gJRudUI3VIEyB4M4ONqDX2qTiNB_LSPNGFu0PXUCN8x7696A)

### Key Takeaways for Interviews

- Know the basic bitwise operators and how to use them.

- Understand how to apply bit manipulation to solve problems.

- Practice problems that involve bit manipulation to become comfortable with these concepts.

  

In coding interviews, demonstrating the ability to use bit manipulation effectively can showcase your understanding of low-level operations and your problem-solving skills, especially in optimization and handling complex data structures.

# Math problems

The problem of "Checking for Primality" involves determining whether a given number is a prime number. A prime number is a natural number greater than 1 that has no positive divisors other than 1 and itself. In other words, a prime number is only divisible by 1 and the number itself.

### Naive Approach
The simplest way to check for primality is to try dividing the number by all smaller numbers:

```python
def is_prime_naive(n):
    if n <= 1:
        return False
    for i in range(2, n):
        if n % i == 0:
            return False
    return True
```

This approach has a time complexity of O(n), which is not efficient for large numbers.

### Efficient Approach
A more efficient method is to check for divisibility only up to the square root of the number. The reasoning is that if `n` is divisible by some number `p`, then `n = p * q`, and without loss of generality, `p <= q`. If both `p` and `q` were greater than the square root of `n`, their product `p * q` would be greater than `n`. So, at least one of those factors must be less than or equal to the square root of `n`, and if we cannot find any factors less than or equal to the square root, `n` must be prime.

```python
def is_prime(n):
    if n <= 1:
        return False
    for i in range(2, int(n**0.5) + 1):
        if n % i == 0:
            return False
    return True
```

This approach reduces the time complexity to O(√n), which is significantly faster, especially for large numbers.

### Edge Cases
- Negative numbers, 0, and 1 are not prime.
- 2 is the only even prime number. For numbers greater than 2, you can optimize further by checking if `n` is even and returning `False` immediately.

### Applications
- Primality testing is a fundamental operation in number theory.
- It has applications in cryptography, especially in algorithms like RSA, where prime numbers are essential for key generation.

### Tips for Interviews
- Understand and explain the reasoning behind checking up to the square root of `n`.
- Discuss potential optimizations.
- Be prepared to handle edge cases correctly.

Checking for primality is a common problem in coding interviews, as it tests your understanding of basic mathematical concepts and your ability to optimize algorithms.

Yes, the primality check algorithm can be further optimized beyond the basic square root approach. Here are some additional optimizations that can be applied:

1. **Check for Small Primes First**: Before the main loop, check divisibility by small primes such as 2, 3, 5, and 7. This can quickly eliminate many composite numbers.

2. **Skip Even Numbers**: If you have already checked for divisibility by 2, you can skip all even numbers in the loop, as they won't be prime (except for 2 itself).

3. **Use a Sieve for Preprocessing**: If you need to check primality for many numbers, consider using a Sieve of Eratosthenes or a similar algorithm for preprocessing to generate a list of primes up to a certain limit.

Here's how you can incorporate these optimizations into the primality check:

```python
def is_prime_optimized(n):
    if n <= 1:
        return False
    if n <= 3:
        return True
    if n % 2 == 0 or n % 3 == 0:
        return False

    i = 5
    while i * i <= n:
        if n % i == 0 or n % (i + 2) == 0:
            return False
        i += 6

    return True
```
# DP and Recursion

Recursion and dynamic programming are powerful concepts in computer science, often used in software engineering interviews to solve complex problems efficiently. Let's break down each concept and provide examples for better understanding.

### Recursion
Recursion is a method where a function calls itself to solve a problem. It's particularly useful for solving problems that can be broken down into smaller, similar subproblems.

**Key Elements of Recursion**:
1. **Base Case**: The condition under which the recursion stops. Without a base case, recursion would continue indefinitely, leading to a stack overflow.
2. **Recursive Case**: The part of the function where it calls itself on a smaller or simpler input.

**Example Problem**: Calculating Factorials.
- The factorial of a number `n` (denoted as `n!`) is `n * (n-1) * (n-2) * ... * 1`. Factorial of `0` is defined as `1`.

```python
def factorial(n):
    if n == 0:         # Base case
        return 1
    else:
        return n * factorial(n - 1)  # Recursive case

# Example: Calculate factorial of 5
print(factorial(5))  # Output: 120
```

### Dynamic Programming (DP)
Dynamic programming is a method for solving complex problems by breaking them down into simpler subproblems and storing the solutions to these subproblems to avoid redundant computations. It's particularly effective for problems with overlapping subproblems and optimal substructure.

**Key Elements of Dynamic Programming**:
1. **Overlapping Subproblems**: The problem can be broken down into subproblems which are reused several times.
2. **Optimal Substructure**: An optimal solution of the problem can be constructed efficiently from optimal solutions of its subproblems.

**Two Main Approaches**:
1. **Top-Down (Memoization)**: This is essentially recursion with caching. Solutions to subproblems are stored in a data structure (like a hash table) and are reused to avoid redundant calculations.
2. **Bottom-Up (Tabulation)**: Iteratively build up the solution by solving all related subproblems first, typically using loops.

**Example Problem**: Fibonacci Sequence.
- The Fibonacci sequence is a series where each number is the sum of the two preceding ones, usually starting with 0 and 1.

**Top-Down Approach (Memoization)**:
```python
def fibonacci(n, memo={}):
    if n in memo:
        return memo[n]
    if n <= 1:
        return n
    memo[n] = fibonacci(n - 1, memo) + fibonacci(n - 2, memo)
    return memo[n]

# Example: Calculate the 5th Fibonacci number
print(fibonacci(5))  # Output: 5
```

**Bottom-Up Approach (Tabulation)**:
```python
def fibonacci(n):
    if n <= 1:
        return n
    fib = [0, 1]
    for i in range(2, n + 1):
        fib.append(fib[i - 1] + fib[i - 2])
    return fib[n]

# Example: Calculate the 5th Fibonacci number
print(fibonacci(5))  # Output: 5
```

### Tips for Interviews
- **Recursion**: Understand how to identify recursive patterns in problems, and always define a clear base case.
- **Dynamic Programming**: Look for overlapping subproblems and optimal substructure. Decide between top-down and bottom-up approaches.
- **Practice**: Solve various problems to recognize patterns and get comfortable with these concepts.

Both recursion and dynamic programming are essential for efficiently solving complex problems and are commonly featured in coding interviews. Understanding and practicing these concepts can significantly enhance problem-solving skills.

# Recognizing problem type

Recognizing the type of problem you're facing and deciding on the appropriate method to solve it is a critical skill in coding interviews. The key is to identify patterns and characteristics that suggest certain approaches like recursion, dynamic programming, or others. Let's discuss how to recognize these problems and provide an example.

### Recognizing Recursion Problems
Problems suited for recursion typically have the following characteristics:
- **Divide into Smaller Instances**: The problem can be broken down into smaller versions of the same problem.
- **Base Case and Recursive Case**: You can identify a simple base case, and the problem has a natural recursive structure.

**Example**: "Given a binary tree, write a function to recursively traverse the tree in preorder and print each node's value."

This problem is recursive because each subtree of a binary tree is a smaller instance of a binary tree. You can visit the root, recursively traverse the left subtree, and then the right subtree.

### Recognizing Dynamic Programming Problems
Dynamic programming is suitable for problems with:
- **Overlapping Subproblems**: The problem can be broken down into subproblems which are solved multiple times.
- **Optimal Substructure**: Solutions to subproblems can be used to construct a solution to the larger problem.

**Example**: "Write a function to compute the nth Fibonacci number. The Fibonacci sequence is defined as follows: the first number of the sequence is 0, the second number is 1, and the nth number is the sum of the (n-1)th and (n-2)th numbers."

This problem has overlapping subproblems (calculating Fibonacci of n requires Fibonacci of n-1 and n-2, which in turn require their preceding Fibonacci numbers) and an optimal substructure (the solution to a larger Fibonacci number can be built from the solutions to smaller Fibonacci numbers).

### Problem Description and Approach
In interviews, problems are often described in a way that hints at the underlying approach. For example:
- If a problem is described as finding a minimum/maximum, count, or whether something is possible (e.g., "minimum cost to reach the end of the array"), and involves making choices at each step, dynamic programming might be a suitable approach.
- If a problem involves searching, exploring all possibilities, or has a natural recursive structure (e.g., "generate all permutations of a given string"), recursion might be the way to go.

### Tips for Interviews
- **Analyze the Problem**: Break down the problem statement and look for key characteristics.
- **Draw Examples**: Work through small examples to understand the problem better.
- **Practice Pattern Recognition**: Solve various problems to get familiar with common patterns and approaches.

By practicing a wide range of problems, you'll start to recognize patterns and become more adept at choosing the appropriate method for solving different types of problems in coding interviews.
