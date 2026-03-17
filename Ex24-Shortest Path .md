# Ex24 Shortest Path and Reachability in a Heritage Town using BFS
## DATE: 21-03-2026
## AIM:
To design and implement a java program that, given a map of attractions in a heritage town connected by walking paths, recommends:
The shortest number of paths (minimum hops) from a starting attraction to a target attraction.
The number of reachable attractions from the same starting point using Breadth-First Search (BFS)


## Algorithm
1. Read n and e, then build an undirected graph using an adjacency list by adding both u→v and v→u for each edge.
2. For shortestPath, run BFS from the start node: mark visited, track distance, and return the distance when the target is reached; if unreachable, return –1.
3. For reachableAttractions, perform DFS starting from the start node, marking every visited node as reachable.
4. Count how many nodes were marked visited to get the number of reachable attractions.
5. Print both the shortest path distance and the total number of reachable attractions from the start node.

## Program:
```JAVA
/*
Program to determine Shortest Path and Reachability in a Heritage Town using BFS
Developed by: Thaanesh V
RegisterNumber: 212223230228
*/
import java.util.*;

public class TouristNavigation {
    
    public static int shortestPath(List<List<Integer>> graph, int start, int target, int n) {
      //Type your code
      boolean[] visited = new boolean[n];
        int[] distance = new int[n];
        Arrays.fill(distance, -1); // -1 means unreachable

        Queue<Integer> queue = new LinkedList<>();
        queue.offer(start);
        visited[start] = true;
        distance[start] = 0;

        while (!queue.isEmpty()) {
            int current = queue.poll();

            // If we reached the target
            if (current == target) {
                return distance[current];
            }

            for (int neighbor : graph.get(current)) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    distance[neighbor] = distance[current] + 1;
                    queue.offer(neighbor);
                }
            }
        }

        // Target unreachable
        return -1;
    }

    public static void reachableAttractions(List<List<Integer>> graph, boolean[] visited, int node) {
        //Type your code
        visited[node] = true;
        for (int neighbor : graph.get(node)) {
            if (!visited[neighbor]) {
                reachableAttractions(graph, visited, neighbor);
            }
        }
    }

    public static int countReachable(boolean[] visited) {
        //Type your code
        int count = 0;
        for (boolean v : visited) {
            if (v) count++;
        }
        return count;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt(), e = sc.nextInt();
        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++) graph.add(new ArrayList<>());

        for (int i = 0; i < e; i++) {
            int u = sc.nextInt(), v = sc.nextInt();
            graph.get(u).add(v);
            graph.get(v).add(u);
        }

        int start = sc.nextInt();
        int target = sc.nextInt();

        int shortest = shortestPath(graph, start, target, n);
        boolean[] visited = new boolean[n];
        reachableAttractions(graph, visited, start);
        int reachable = countReachable(visited);

        System.out.println("Shortest path from start to target: " + shortest);
        System.out.println("Total reachable attractions from start: " + reachable);
    }
}

```

## Output:
<img width="1265" height="404" alt="image" src="https://github.com/user-attachments/assets/5092563e-d395-40af-8729-a7d7e1ca3cf0" />



## Result:
The program has been successfully implemented and executed.
It correctly computes:
The shortest number of paths (minimum hops) between two attractions.
The total number of reachable attractions from a given starting point using BFS traversal.
