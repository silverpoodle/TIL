###  깊이 우선 탐색(Depth-First Search)

> **깊이 우선 탐색(DFS)은 그래프의 정점을 탐색하는 알고리즘 중 하나로,** 
> **시작 정점에서부터 더 이상 방문할 수 있는 정점이 없을 때까지 최대한 깊게 탐색하는 방식**

<img src="https://raw.githubusercontent.com/silverpoodle/TIL/main/images/image-20240217230541204.png" alt="image-20240217230541204" style="zoom:80%;" />



#### 스택(Stack)을 이용한 구현

<img src="https://miro.medium.com/v2/resize:fit:1400/1*EpJM4d8ifViCuVz2Kmtmzw.png" alt="Depth-First Search (DFS) Algorithm With Python | by Fahadul Shadhin | Geek  Culture | Medium" style="zoom:50%;" />



```
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
import java.util.Stack;

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

    // DFS 알고리즘
    public void DFSWithAdjacencyList(int start) {
        boolean[] visited = new boolean[V]; // 방문 여부를 저장하는 배열
        Stack<Integer> stack = new Stack<>();

        visited[start] = true;
        stack.push(start);

        while (!stack.isEmpty()) {
            start = stack.pop();
            System.out.print(start + " ");

            for (Integer neighbor : adjList[start]) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    stack.push(neighbor);
                }
            }
        }
    }
}

public class DFSExample {
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
        graph.DFSWithAdjacencyList(0);
    }
}
```





#### 2. 인접행렬

```java
import java.util.Stack;

public class DFSWithAdjacencyMatrix {

    // 그래프의 인접행렬을 사용한 DFS 메서드
    public static void dfs(int[][] graph, int start) {
        int vertices = graph.length;
        boolean[] visited = new boolean[vertices];
        Stack<Integer> stack = new Stack<>();

        // 시작 정점을 방문하고 스택에 추가
        visited[start] = true;
        stack.push(start);

        while (!stack.isEmpty()) {
            int currentVertex = stack.pop();
            System.out.print(currentVertex + " ");

            // 인접한 정점들을 방문하고 스택에 추가
            for (int i = 0; i < vertices; i++) {
                if (graph[currentVertex][i] == 1 && !visited[i]) {
                    visited[i] = true;
                    stack.push(i);
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
        dfs(adjacencyMatrix, 0);
    }
}
```





#### DFS 진행과정

```less
DFS(0)을 호출하여 시작 정점을 스택에 추가
스택: [0]
방문: [true, false, false, false, false]

스택에서 0을 꺼내 출력하고 인접한 정점 1과 2를 스택에 추가
스택: [1, 2]
방문: [true, true, true, false, false]
출력: 0

스택에서 2를 꺼내 출력하고 인접한 정점 4를 스택에 추가
스택: [1, 4]
방문: [true, true, true, false, true]
출력: 2

스택에서 4를 꺼내 출력
스택: [1]
방문: [true, true, true, false, true]
출력: 4

스택에서 1을 꺼내 출력하고 인접한 정점 3을 스택에 추가
스택: [3]
방문: [true, true, true, true, true]
출력: 1

스택에서 3을 꺼내 출력
스택: []
방문: [true, true, true, true, true]
출력: 3

// 결과: 0 2 4 1 3
```