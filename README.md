<h1>ExpNo 4 : Implement A* search algorithm for a Graph</h1> 
<h3>Name: Vasanth kumar V     </h3>
<h3>Register Number: 2305002027          </h3>
<H3>Aim:</H3>
<p>To ImplementA * Search algorithm for a Graph using Python 3.</p>
<H3>Algorithm:</H3>


// A* Search Algorithm
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

## PROGRAM
```python
from collections import defaultdict

def a_star(start, goal, graph, H):
    open_set = {start}
    closed_set = set()
    g = {start: 0}
    parent = {start: None}

    while open_set:
        # Pick node with minimum f = g + h
        n = min(open_set, key=lambda x: g[x] + H[x])

        if n == goal:
            path = []
            while n is not None:
                path.append(n)
                n = parent[n]
            path.reverse()
            print("Path found:", path)
            return

        open_set.remove(n)
        closed_set.add(n)

        for (m, cost) in graph[n]:
            if m in closed_set:
                continue
            new_g = g[n] + cost
            if m not in open_set or new_g < g.get(m, float('inf')):
                g[m] = new_g
                parent[m] = n
                open_set.add(m)

    print("Path does not exist!")


# --- Input section ---
graph = defaultdict(list)
n, e = map(int, input("Enter number of nodes and edges: ").split())

print("\nEnter each edge in the format: node1 node2 cost")
for _ in range(e):
    u, v, cost = input().split()
    cost = int(cost)
    graph[u].append((v, cost))
    graph[v].append((u, cost))  # undirected graph

H = {}
print("\nEnter heuristic value for each node:")
for _ in range(n):
    node, h = input().split()
    H[node] = int(h)

start = input("\nEnter start node: ")
goal = input("Enter goal node: ")

print("\n--- A* Search Result ---")
a_star(start, goal, graph, H)


```

SAMPLE GRAPH I
<img width="233" height="493" alt="Screenshot 2025-10-08 140420" src="https://github.com/user-attachments/assets/33c60b1e-227e-4fd0-a742-5d8453acb824" />


SAMPLE INPUT
 5 7 <br>
 A B 1 <br>
 A C 3 <br>
 B C 1 <br>
 B D 4 <br>
 C D 2 <br>
 D E 5 <br>
 C E 6 <br>
 A 10 <br>
 B 8 <br>
 C 5 <br>
 D 7 <br>
 E 0 <br>
 A <br>
 E <br>
 <br>
<hr>
Sample Output


<img width="621" height="740" alt="Screenshot 2025-10-08 140048" src="https://github.com/user-attachments/assets/5f25eb20-fbb3-4b39-8948-2cfd253089cd" />




<hr>
<h2>Sample Graph II</h2>
<hr>

<img width="252" height="505" alt="Screenshot 2025-10-08 140536" src="https://github.com/user-attachments/assets/e6927252-5c14-4d69-b028-daa543547404" />


<hr>
<h2>Sample Input</h2>
<hr>
 5 6 <br>
 S A 2 <br>
 S B 4 <br>
 A C 7 <br>
 B C 1 <br>
 C G 3 <br>
 B G 8 <br>
 S 7 <br>
 A 6 <br>
 B 2 <br>
 C 1 <br>
 G 0 <br>
 S <br>
 G <br>
<hr>

SAMPLE OUTPUT

<img width="634" height="717" alt="Screenshot 2025-10-08 140856" src="https://github.com/user-attachments/assets/40caeeeb-e14f-4ba5-9a5f-1662649ab003" />

## RESULT
Thus the above python program for A* Search has executed successfully.
