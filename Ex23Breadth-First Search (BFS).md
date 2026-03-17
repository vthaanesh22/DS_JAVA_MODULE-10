# Ex23 Breadth-First Search (BFS) Traversal of a City Junction Map
## DATE: 18-03-2026
## AIM:
To design and implement a java program to perform Breadth-First Search (BFS) traversal on a city’s junction map represented as a graph, and find all reachable locations from a given source junction.
## Algorithm
1. Read n (number of nodes) and e (number of edges), then create an adjacency list with n empty lists.
2. For each edge, read its endpoints u and v, and add both u→v and v→u in the graph using addEdge.
3. Read the source node src for BFS traversal.
4. In bfs, mark the source as visited, push it into a queue, and begin traversal.
5. While the queue is not empty, pop a node, print it, and push all its unvisited neighbors into the queue, marking them visited.

## Program:
```JAVA
/*
Program to perform Breadth-First Search (BFS) traversal on a city’s junction map represented as a graph
Developed by: Thaanesh V
RegisterNumber: 212223230228
*/
import java.util.*;

public class EmergencyRouteBFS {
    public static void addEdge(List<List<Integer>> g, int u, int v) {
        //Type your Code
        g.get(u).add(v);
        g.get(v).add(u);
    }

    public static void bfs(List<List<Integer>> g, int src, boolean[] visited) {
        //Type your Code
        Queue<Integer> q = new LinkedList<>();
        q.offer(src);
        visited[src] = true;
        while (!q.isEmpty()) {
            int curr = q.poll();
            System.out.print(curr + " ");
            for (int neighbor : g.get(curr)) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    q.offer(neighbor);
                }
            }
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(), e = sc.nextInt();
        List<List<Integer>> g = new ArrayList<>();
        for (int i = 0; i < n; i++) g.add(new ArrayList<>());
        for (int i = 0; i < e; i++) addEdge(g, sc.nextInt(), sc.nextInt());
        int src = sc.nextInt();
        bfs(g, src, new boolean[n]);
    }
}

```

## Output:
<img width="1266" height="395" alt="image" src="https://github.com/user-attachments/assets/734251c8-9d92-4fe6-9233-345c71628542" />



## Result:
The program has been successfully implemented and executed.
It performs Breadth-First Search (BFS) traversal on a city junction map and correctly lists all reachable locations from the given source node.
