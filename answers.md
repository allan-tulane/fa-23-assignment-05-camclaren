# CMPS 2200 Assignment 5
## Answers

**Name:**Cameron McLaren


- **1a.**
**(log_d(dn-n+1)) - 1**
each level has d^i nodes (at level i) --> geometric series where max depth would be d^k <= n and the sum of the series is (d^(k + 1) - 1)/(d - 1) <= n
hence:
d^(k + 1) - 1 <= n(d - 1)
d^(k + 1) <= n(d - 1) + 1
k + 1 <= log_d(nd - d + 1)
k <= log_d(nd - d + 1) - 1

- **1b.**
The function `insert` would have a work of O(log_d(n)) while the `delete-min` function would have a work of O(d * log_d(n)).

- **1c.**
Combine work of `delete-min` and `insertion` function:
`delete-min`: O(|E|log_d(|V|))
`insertion`: O((|V|d)log_d(|V|))
total: O(|E|log_d(|V|)) + O((|V|d)log_d(|V|)) --> O((|V|d + |E|)log_d|V|)

- **1d.**
|V| = |E|^(1/ (1 + e))

O(|E|^(1/ (1 + e))d + |E|) * log_d|E|^(1/ (1+e)) = O(|E|)
log_d|E|^(1/ (1 + e)) = (1/ 1 + e) * log_d(|E|)
(|E|^(1/ (1 + e))) d/(1 + e)log_d(|E|) = |E|
|E|^(1/ (1 + e))d + |E| = |E|(1 + e)
|E|^(1/ (1 + e))d = |E|(1 + e)
|E|^(1/ (1 + e))d = |E|(1 + e) - |E|
d = |E|e / |E|^(1/ (1 + e))

- **2a.**
I don't fully understand this question

- **2b.**
The relationship between the two is that APSP(i,j,2) is the minimum of APSP(i,j,1) and APSP(i,2,1) + APSP(2,j,1)

- **2c.**
The optimal substructure property for APSP(i,j,k-1) and APSP(i,k,k-1) + APSP(k,j,k-1). This is due to the shortest path being from i to j using only vertices 0,1,...,k is the same as the shortest path using vertices 0,1,...,k-1.

- **2d.**
If we do top-down memoization, the number of distinct subproblems is n * n * n, where n is the number of vertices in the graph. Therefore, the work of the algorithm is O(n^3).

- **2e.**
The work of the algorithm is O(n^3), and the work of Dijkstra is O(n^2 logb + nE) --> E = num edges in graph

If the graph is dense, then the dynamic algorithm is better than Dijkstra's, but if the graph is sparse then vice versa is true.


- **3a.**
No, the MST problem solution is not guaranteed to be one that works for the MMET problem. MST aims to minimize the sum of edge weight, but does not factor in the weight of any specific edge; meanwhile, MMET looks to minmize the maximum weight among all the tree edges.

- **3b.**
    1. Find the Minimum Spanning Tree (MST) T1 using a standard MST algorithm
    2. Let `max` be the weight of the maximum weight edge in T1
    3. For each edge `e` in T1:
        a. If `e` is not the maximum weight edge in T1, mark it as ineligible
    4. For each ineligible edge `e`:
        a. Find an alternative path that doesn't include `e`
        b. If the alternative path has a weight less than `max`, add it to the set of eligible edges
    5. Let `new_e` be the edge with the minimum weight in the set of eligible edges
    6. Replace the maximum weight edge in T1 with `new_e` to get a new spanning tree T2
    7. Return T2 as the next best tree


- **3c.**
E = num edges
V = num vertices

W(n) for each step from 3b:
1. O(ElogV) --> work for Prim's or Kruskal's algorithms
2. O(E) --> iterating through edges of T1
3. O(E) --> iterating through edges of T1 again
4. O(V + E) --> may involve traversing graph, therefore worst case scenario
5. O(E) --> selecting from set of eligible edges
6. O(1) --> updating tree structure
7. O(1) --> return new tree

W(n) = O(ElogV) + O(E) + O(E) + O(V + E) + O(E)
     = **O(ElogV)** --> O(ElogV) is the largest, therefore it dominates the others
