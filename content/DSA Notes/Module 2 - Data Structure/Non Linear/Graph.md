Graphs (Why They Matter)  
  
> [!abstract]  
> Graphs provide a clean mathematical way to model relationships between objects.  

  
# 14. Motivation: Map Coloring  
  
Problem:  
![[Pasted image 20260626162734.png|296]]
- Color countries so neighbors differ  
- Minimize number of colors  
  
## Graph Representation  
  
- Vertex = country  
- Edge = shared border  
  
Simplifies problem:  
- removes irrelevant geographic detail  
- keeps only adjacency structure  
  
---  
  
# 15. Real-World Applications  
  
Graph coloring appears in:  
  
- exam scheduling  
- register allocation  
- frequency assignment  
- resource allocation problems  
  
---  
  
# 16. Formal Definition of a Graph  
  
A graph is:  
  
$$
G = (V, E)  
$$
  
Where:  
- V = vertices (nodes)  
- E = edges (connections)  
  
## Types of graphs  
  
### Undirected Graph  
- Edge: {u, v}  
- Symmetric relation  
![[Pasted image 20260626161926.png|261]]
  
### Directed Graph  
- Edge: (u, v)  
- Asymmetric relation  

![[Pasted image 20260626162312.png|253]]
  
Example:  
- Web graph (billions of nodes)  

  
# 17. Graph Representations  
  
## 1. Adjacency Matrix  
  
$$
A[i][j] =  
\begin{cases}  
1 & \text{if edge exists}\\  
0 & \text{otherwise}  
\end{cases}  
$$
  
### Properties:  
- Space: O(n²)  
- Fast edge lookup: O(1)  
- Wasteful for sparse graphs
  
## 2. Adjacency List  
  
- Each vertex stores list of neighbors  
- Space: O(|V| + |E|)  
  
### Properties:  
- Efficient for sparse graphs  
- Fast neighbor traversal  
- Slower edge lookup than matrix  
  
---  
  
> [!important]  
> Real-world graphs (like the web) are sparse → adjacency lists are preferred.  
  
---  
  
# 18. Sparse vs Dense Graphs  
  
| Type   | Condition |     |     |     |     |     |
| ------ | --------- | --- | --- | --- | --- | --- |
| Sparse |           | E   | ≈   | V   |     |     |
| Dense  |           | E   | ≈   | V   | ²   |     |
  
---  
  
# 19. Key Insight  
  
> [!summary]  
> Choice of representation depends on structure of data:  
- Dense graph → adjacency matrix  
- Sparse graph → adjacency list  
  
---  
  
# 20. Final Takeaways  
### Graphs:  
- Model relationships cleanly  
- Allow efficient algorithm design  
- Representation choice is critical