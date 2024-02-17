### 너비 우선 탐색(Breath-First-Search)

> **그래프의 정점을 탐색하는 알고리즘 중 하나로, **
> **시작 정점에서부터 인접한 정점을 모두 방문한 후에 그 다음 단계의 인접 정점들을 차례로 방문하는 방식**

<img src="https://raw.githubusercontent.com/silverpoodle/TIL/main/images/image-20240215222519580.png" alt="image-20240215222519580" style="zoom:80%;" />



#### 큐(Queue) 를 이용한 구현

![image-20240217222338278](https://raw.githubusercontent.com/silverpoodle/TIL/main/images/image-20240217222338278.png)



```math
 예시 그래프
               0
              / \
             1   2
             |   |
             3   4
```



#### 1. 인접 리스트

```java
import java.util.LinkedList;
import java.util.Queue;

class Graph {
    private int V; // 정점의 수
    private LinkedList<Integer>[] adjList; // 인접 리스트

    // 그래프 초기화
    public Graph(int v) {
        V = v;
        adjList = new LinkedList[v];
        for (int i = 0; i < v; ++i)
            adjList[i] = new LinkedList();
    }

    // 간선 추가
    public void addEdge(int v, int w) {
        adjList[v].add(w);
    }

    // BFS 알고리즘
    public void BFSWithAdjacencyList (int start) {
        boolean[] visited = new boolean[V]; // 방문 여부를 저장하는 배열
        Queue<Integer> queue = new LinkedList<>();

        visited[start] = true;
        queue.add(start);

        while (!queue.isEmpty()) {
            start = queue.poll();
            System.out.print(start + " ");

            for (Integer neighbor : adjList[start]) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.add(neighbor);
                }
            }
        }
    }
}

public class BFSExample {
    public static void main(String[] args) {
        Graph graph = new Graph(5);
        /* 그래프를 나타내는 Graph 클래스를 생성
            0: []
            1: []
            2: []
            3: []
            4: []
        */
        
        graph.addEdge(0, 1);
        graph.addEdge(0, 2);
        graph.addEdge(1, 3);
        graph.addEdge(2, 4);
        /* addEdge(0, 1)을 호출하여 정점 0과 1을 연결
            0: [1]
            1: []
            2: []
            3: []
            4: []

            addEdge(0, 2)을 호출하여 정점 0과 2를 연결
            0: [1, 2]
            1: []
            2: []
            3: []
            4: []

            addEdge(1, 3)을 호출하여 정점 1과 3을 연결
            0: [1, 2]
            1: [3]
            2: []
            3: []
            4: []

            addEdge(2, 4)를 호출하여 정점 2와 4를 연결
            0: [1, 2]
            1: [3]
            2: [4]
            3: []
            4: []
        */
        graph.BFS(0);
    }
}
```



#### 2. 인접행렬

```java
import java.util.LinkedList;
import java.util.Queue;

public class BFSWithAdjacencyMatrix {

    // 그래프의 인접행렬을 사용한 BFS 메서드
    public static void bfs(int[][] graph, int start) {
        int vertices = graph.length;
        boolean[] visited = new boolean[vertices];
        Queue<Integer> queue = new LinkedList<>();

        // 시작 정점을 방문하고 큐에 추가
        visited[start] = true;
        queue.offer(start);

        while (!queue.isEmpty()) {
            int currentVertex = queue.poll();
            System.out.print(currentVertex + " ");

            // 인접한 정점들을 방문하고 큐에 추가
            for (int i = 0; i < vertices; i++) {
                if (graph[currentVertex][i] == 1 && !visited[i]) {
                    visited[i] = true;
                    queue.offer(i);
                }
            }
        }
    }

    public static void main(String[] args) {
            /* 그래프의 인접행렬
               0 1 2 3 4
            0 [0 1 1 0 0]
            1 [1 0 0 1 0]
            2 [1 0 0 1 1]
            3 [0 1 1 0 1]
            4 [0 0 1 1 0]
            */
        int[][] adjacencyMatrix = {
                {0, 1, 1, 0, 0},
                {1, 0, 0, 1, 0},
                {1, 0, 0, 1, 1},
                {0, 1, 1, 0, 1},
                {0, 0, 1, 1, 0}
        };
        bfs(adjacencyMatrix, 0);
    }
}
```



#### BFS 진행과정

```less
BFS(0)을 호출하여 시작 정점을 큐에 추가
큐: [0]
방문: [true, false, false, false, false]

큐에서 0을 꺼내 출력하고 인접한 정점 1과 2를 큐에 추가
큐: [1, 2]
방문: [true, true, true, false, false]
출력: 0

큐에서 1을 꺼내 출력하고 인접한 정점 3을 큐에 추가
큐: [2, 3]
방문: [true, true, true, true, false]
출력: 1

큐에서 2를 꺼내 출력하고 인접한 정점 4를 큐에 추가
큐: [3, 4]
방문: [true, true, true, true, true]
출력: 2

큐에서 3을 꺼내 출력
큐: [4]
방문: [true, true, true, true, true]
출력: 3

큐에서 4를 꺼내 출력
큐: []
방문: [true, true, true, true, true]
출력: 4


// 결과: 0 1 2 3 4
```

