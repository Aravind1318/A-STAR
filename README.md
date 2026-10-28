<h1>ExpNo 4 : Implement A* search algorithm for a Graph</h1> 
<h3>Name: ARAVIND P </h3>
<h3>Register Number: 212224240015 </h3>
<H3>Aim:</H3>
<p>To ImplementA * Search algorithm for a Graph using Python 3.</p>
<H3>Algorithm:</H3>


1.  Initialize the open list
2.  Initialize the closed list
    put the starting node on the open 
    list (you can leave its f at zero)

3.  while the open list is not empty
    a) find the node with the least f on 
       the open list, call it "q"

    b) pop q off the open list
  
    c) generate q's 8 successors and set their 
       parents to q
   
    d) for each successor
        i) if successor is the goal, stop search
         ii) else, compute both g and h for successor
          successor.g = q.g + distance between 
                              successor and q
          successor.h = distance from goal to 
          successor (This can be done using many 
          ways, we will discuss three heuristics- 
          Manhattan, Diagonal and Euclidean 
          Heuristics)
          
   successor.f = successor.g + successor.h

iii) if a node with the same position as 
            successor is in the OPEN list which has a 
           lower f than successor, skip this successor

iV) if a node with the same position as 
            successor  is in the CLOSED list which has
            a lower f than successor, skip this successor
            otherwise, add  the node to the open list
     end (for loop)
  
e) push q on the closed list
    end (while loop)



<hr>
<h2>Sample Graph </h2>

<img width="1618" height="972" alt="Heuristic Network Graph Diagram" src="https://github.com/user-attachments/assets/fe6f5a59-702f-48d7-8c54-374f3784c7ab" />

<hr>


### Program

```python
import heapq
from collections import defaultdict

def aStarAlgo(graph, start, goal, H_dist):
    open_set = [(H_dist[start], start)]
    parents = {start: None}
    g = {start: 0}

    while open_set:
        f, node = heapq.heappop(open_set)

        if node == goal:
            path = []
            while node is not None:
                path.append(node)
                node = parents[node]
            path.reverse()
            print("Path found:", path)
            return

        for neighbour, weight in graph[node]:
            new_cost = g[node] + weight

            if neighbour not in g or new_cost < g[neighbour]:
                g[neighbour] = new_cost
                parents[neighbour] = node
                heapq.heappush(open_set, (new_cost + H_dist[neighbour], neighbour))

    print("Path does not exist!")

graph = defaultdict(list)

n, e = map(int, input("Enter the number of nodes and edges: ").split())

for i in range(e):
    u, v, cost = input(f"Enter edge {i+1} (u v cost): ").split()
    cost = int(cost)
    graph[u].append((v, cost))
    graph[v].append((u, cost))

H_dist = {}

print("Enter the heuristic values:")
for i in range(n):
    node, h = input().split()
    H_dist[node] = int(h)

start = input("Enter the starting node: ")
goal = input("Enter the goal node: ")

aStarAlgo(graph, start, goal, H_dist)
```

### Sample Input

```text
Enter the number of nodes and edges: 6 7
Enter edge 1 (u v cost): S A 2
Enter edge 2 (u v cost): S B 5
Enter edge 3 (u v cost): A C 2
Enter edge 4 (u v cost): A D 6
Enter edge 5 (u v cost): B D 1
Enter edge 6 (u v cost): C G 5
Enter edge 7 (u v cost): D G 2
Enter the heuristic values:
S 6
A 5
B 3
C 5
D 2
G 0
Enter the starting node: S
Enter the goal node: G
```

### Output

```text
Path found: ['S', 'B', 'D', 'G']
```

<hr>

<h3>Result:</h3>

<hr>

<p>Thus, a weighted graph was constructed and the implementation of the A* Search algorithm was completed successfully to find a path from the starting node to the goal node using edge costs and heuristic values.</p>
