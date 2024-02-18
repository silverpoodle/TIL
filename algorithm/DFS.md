###  깊이 우선 탐색(Depth-First Search)

> **깊이 우선 탐색(DFS)은 그래프의 정점을 탐색하는 알고리즘 중 하나로,** 
> **시작 정점에서부터 더 이상 방문할 수 있는 정점이 없을 때까지 최대한 깊게 탐색하는 방식**

<img src="https://raw.githubusercontent.com/silverpoodle/TIL/main/images/image-20240217230541204.png" alt="image-20240217230541204" style="zoom:80%;" />



#### 재귀를 이용한 구현 (추천)

```less
1. 동작검증 쉬움
	하나의 조합을 만들어 비교하는 과정을 반복 -> 정답 비교가 쉽고 빠름
2. BFS 의 경우 여러개의 조합을 동시에 만들며 한칸씩 비교하기 때문에 언제부터 틀렸는지 분석하기 쉽지 않음

but!!!
시간 초과 위험성 -> 수행 시간 관점에서는 복불복
```



```java
import java.util.ArrayList;
import java.util.List;

class Node {
    int value;
    List<Node> neighbors;

    public Node(int value) {
        this.value = value;
        this.neighbors = new ArrayList<>();
    }

    public void addNeighbor(Node neighbor) {
        this.neighbors.add(neighbor);
    }
}

public class DFS {
    public static void main(String[] args) {
        // 그래프 생성
        Node node0 = new Node(0);
        Node node1 = new Node(1);
        Node node2 = new Node(2);
        Node node3 = new Node(3);
        Node node4 = new Node(4);

        node0.addNeighbor(node1);
        node0.addNeighbor(node2);
        node1.addNeighbor(node3);
        node2.addNeighbor(node4);

        // DFS 호출
        dfs(node0, new boolean[5]);
    }

    public static void dfs(Node node, boolean[] visited) {
        // 현재 노드 방문 처리
        System.out.println(node.value + " ");
        visited[node.value] = true;

        // 인접 노드들에 대해 재귀적으로 DFS 호출
        for (Node neighbor : node.neighbors) {
            if (!visited[neighbor.value]) {
                dfs(neighbor, visited);
            }
        }
    }
}
```

```less

그래프 초기화 및 노드 생성:
- 노드 0부터 노드 4까지 5개의 노드를 생성하고, 각 노드의 이웃 노드를 설정
- node0의 이웃은 node1과 node2, node1의 이웃은 node3, node2의 이웃은 node4

1. DFS 호출 시작:
dfs 메서드를 호출하고, 시작 노드로 node0을 전달
방문 여부를 나타내는 배열 visited를 초기화합니다. 초기에는 모든 원소가 false
[false, false, false, false, false]


2. DFS 함수 내부 (시작 노드 0):
현재 노드 node0를 방문 처리하고, visited 배열의 해당 인덱스를 true로 설정합
현재 노드의 이웃 노드들을 확인
[true, false, false, false, false]


3. DFS 함수 내부 (이웃 노드 1):
node0의 이웃인 node1을 방문하지 않았다면 dfs를 재귀적으로 호출
현재 노드 node1을 방문 처리하고, visited 배열의 해당 인덱스를 true로 설정
현재 노드 node1의 이웃 노드인 node3을 확인
[true, true, false, false, false]


4. DFS 함수 내부 (이웃 노드 3):
node1의 이웃인 node3을 방문하지 않았다면dfs를 재귀적으로 호출
현재 노드 node3을 방문 처리하고, visited 배열의 해당 인덱스를 true로 설정
현재 노드 node3의 이웃 노드는 없음!!!
[true, true, false, true, false]


5. DFS 함수 내부 (이웃 노드 2):
node0의 다음 이웃인 node2를 방문하지 않았다면 dfs를 재귀적으로 호출
현재 노드 node2을 방문 처리하고, visited 배열의 해당 인덱스를 true로 설정
현재 노드 node2의 이웃 노드인 node4를 확인
[true, true, true, true, false]


6. DFS 함수 내부 (이웃 노드 4):
node2의 이웃인 node4를 방문하지 않았다면, dfs를 재귀적으로 호출
현재 노드 node4을 방문 처리하고, visited 배열의 해당 인덱스를 true로 설정
현재 노드 node4의 이웃 노드는 없음!!!
[true, true, true, true, true]


7. DFS 함수 종료: 모든 노드를 방문하고 dfs 함수가 종료

//결과: 0 1 2 3 4
```





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