# Ex25 Finding the Fastest Route to a Charging Station using Dijkstra’s Algorithm
## DATE: 21-03-2026
## AIM:
To design and implement a java program that helps an electric vehicle (EV) find the shortest travel time from its current block to the nearest charging station using Dijkstra’s shortest path algorithm.
## Algorithm
1. Read n nodes and m weighted edges, then build an undirected graph where each edge stores the neighbor and travel time.
2. Read the source node and the set of charging-station nodes.
3. Initialize a distance array with infinity and set the distance of the source to 0.
4. Use Dijkstra’s algorithm: push (source,0) into a min-heap, repeatedly extract the node with the smallest time, relax its neighbors, and update distances.
5. The moment a charging-station node is polled from the heap, return its travel time; if none is reachable, return –1.

## Program:
```JAVA
/*
Program to find the Fastest Route to a Charging Station using Dijkstra’s Algorithm
Developed by: Thaanesh V
RegisterNumber: 212223230228
*/
import java.util.*;

public class EVChargingNavigation {

    static class Pair {
        int node, time;
        Pair(int node, int time) {
            this.node = node;
            this.time = time;
        }
    }

    static int findNearestChargingStation(int n, List<List<Pair>> graph, int source, Set<Integer> stations) {
        //Type your code
        int[] dist = new int[n];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[source] = 0;

        // Min-heap for (time, node)
        PriorityQueue<Pair> pq = new PriorityQueue<>(Comparator.comparingInt(a -> a.time));
        pq.offer(new Pair(source, 0));

        while (!pq.isEmpty()) {
            Pair current = pq.poll();
            int node = current.node;
            int time = current.time;

            // Skip outdated entries
            if (time > dist[node]) continue;

            // If current node is a charging station, return its distance
            if (stations.contains(node)) {
                return time;
            }

            // Explore neighbors
            for (Pair neighbor : graph.get(node)) {
                int newTime = time + neighbor.time;
                if (newTime < dist[neighbor.node]) {
                    dist[neighbor.node] = newTime;
                    pq.offer(new Pair(neighbor.node, newTime));
                }
            }
        }

        // If no charging station is reachable
        return -1;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        int n = sc.nextInt(), m = sc.nextInt();
        List<List<Pair>> graph = new ArrayList<>();
        for (int i = 0; i < n; i++) graph.add(new ArrayList<>());

        for (int i = 0; i < m; i++) {
            int u = sc.nextInt(), v = sc.nextInt(), w = sc.nextInt();
            graph.get(u).add(new Pair(v, w));
            graph.get(v).add(new Pair(u, w)); // Undirected
        }

        int source = sc.nextInt();
        int k = sc.nextInt();
        Set<Integer> stations = new HashSet<>();
        for (int i = 0; i < k; i++) stations.add(sc.nextInt());

        System.out.println(findNearestChargingStation(n, graph, source, stations));
    }
}

```

## Output:
<img width="1265" height="485" alt="image" src="https://github.com/user-attachments/assets/94c4011a-ba93-4777-9931-87e0331f45a5" />



## Result:
The program has been successfully implemented and executed.
It uses Dijkstra’s algorithm to determine the shortest travel time from the EV’s current location to the nearest charging station and correctly handles cases where no station is reachable.
