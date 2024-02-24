## 완전탐색 (Exhaustive Search)

>**모든 가능한 경우의 수**를 탐색하여 최적의 결과를 찾는 방법
>
>모든 가능성을 고려하기 때문에 최적의 해를 찾을 수 있지만 경우의 수가 매우 많은 경우 시간과 메모리의 부담

<br/>

|     알고리즘      | 특징                                                         | 장점                                             | 단점                                            |
| :---------------: | ------------------------------------------------------------ | ------------------------------------------------ | :---------------------------------------------- |
|  **브루트 포스**  | 모든 가능한 조합을 시도하여 원하는 결를 찾음                 | 구현이 간단하며, 모든 경우를 탐색할 수 있음      | 시간 복잡도가 크게 증가할 수 있음               |
|   **백트래킹**    | 조건에 맞지 않으면 해당 가지치기 후 다른 경우로 이동         | 일부 경우의 가지치기를 통해 효율적으로 탐색 가능 | 스택오버플로우 발생할 수 있음                   |
|  **비트 마스크**  | 모든 경우의 수를 이진수로 표현하고 비트 연산을 통해 원하는 결과를얻 | 메모리 사용이 효율적이며, 연산 속도가 빠름       | 문제에 따라 비트 표현이 복잡해질 수 있음        |
|   **재귀 함수**   | 재귀적 호출을 통해 모든 경우를 탐색                          | 코드의 간결성과 가독성이 좋음                    | 깊은 재귀 호출 시 스택 오버플로우 가능성이 있음 |
| **순열 알고리즘** | 순열을 생성하여 문제 해결<br />(순열은 서로 다른 n개 중에서 r개를 선택하여 나열하는 방법) | 특정 순서의 순열을 쉽게 생성 가능                | 경우의 수가 많을 경우 시간 오래걸림             |
|      **DFS**      | 깊이 우선 탐색을 사용하여 가능한 모든 경로를 탐색            | 그래프 구조에서 높은 유연성을 제공               | 최악의 경우 모든 경로를 탐색해야 할 수 있음     |
|      **BFS**      | 너비 우선 탐색을 사용하여 가능한 모든 상태를 탐색            | 최단 경로 문제에서 효과적으로 사용 가능          | 최악의 경우 모든 경로를 탐색해야 할 수 있음     |

<br/>

### 브루트 포스 (Brute Force)

> 단순한 힘 = 냅다 다 해보기..><
>
> 1. **for / while 루프** 활용
> 2. **재귀함수**

<img src="https://slideplayer.com/slide/8709386/26/images/2/The+Brute-Force+Algorithms.jpg" alt="6.4: The Brute-Force Algorithms - ppt video online download" style="zoom:67%;" />

> 모든 정점이 연결된 그래프에서 모든 정점을 방문하고 원래 출발지로 돌아오는 최소비용의 경로를 구하는 문제

<br/><br/>



### 비트마스트 (Bit Mask)

> 이진수 표현을 활용하여 집합의 부분집합을 나타내는 기법으로, 비트 연산을 사용하여 집합 연산을 간결하게 처리
>
> *집합에 속하는 원소의 인덱스를 이진수의 비트로 표현하고 해당 비트가 1이면 집합에 속하는 것으로 간주*

| 연산자 | 설명                                           | 예시                  |
| ------ | ---------------------------------------------- | --------------------- |
| `&`    | AND 연산: 두 비트가 모두 1이면 1, 아니면 0     | `1010 & 1100 = 1000`  |
| `|`    | OR 연산: 두 비트 중 하나라도 1이면 1, 아니면 0 | `1010 \| 1100 = 1110` |
| `^`    | XOR 연산: 두 비트가 다르면 1, 같으면 0         | `1010 ^ 1100 = 0110`  |
| `~`    | NOT 연산: 비트를 반전                          | `~1010 = 0101`        |
| `<<`   | 왼쪽 시프트: 비트를 왼쪽으로 이동              | `1010 << 2 = 1000`    |
| `>>`   | 오른쪽 시프트: 비트를 오른쪽으로 이동          | `1010 >> 2 = 0010`    |

```sql
 {true, false, true, false}인 배열을 2진수로 1010으로 표현하고, 다시 십진수로 변환하면 10
```

`백준 2098, 1102`



<br/><br/>

### 외판원 문제 (TSP)

```sql
도시를 방문하는 경로의 모든 경우의 수를 찾아야 하기 때문에, 방문한 도시와 방문하지 않은 도시를 계속해서 추적해야 한다.
방문한 도시에 대한 정보를 배열을 사용해서 저장하게 되면, 도시의 수가 많아질수록 메모리를 굉장히 많이 차지하게 된다.

배열 대신에 비트마스킹을 사용하면 단일 정수를 사용해서 방문한 도시 집합을 나타낼 수 있다!
```

1. Brute Force

   ```java
   public class Main {
       static int N;
       static int[][] W;
       static int[][] dp;
   
       public static void main(String[] args) {
           Scanner sc = new Scanner(System.in);
           N = sc.nextInt();
           W = new int[N][N];
           dp = new int[N][1 << N];
   
           for (int i = 0; i < N; i++) {
               for (int j = 0; j < N; j++) {
                   W[i][j] = sc.nextInt();
               }
           }
   
           System.out.println(tsp(0, 1));
       }
   
       static int tsp(int current, int visited) {
           if (visited == (1 << N) - 1) {
               if (W[current][0] == 0) return Integer.MAX_VALUE / 2; // 시작 도시로 갈 수 없는 경우
               return W[current][0];
           }
   
           if (dp[current][visited] != 0) return dp[current][visited];
   
           int result = Integer.MAX_VALUE / 2;
   
           for (int i = 0; i < N; i++) {
               if ((visited & (1 << i)) == 0 && W[current][i] != 0) {
                   result = Math.min(result, W[current][i] + tsp(i, visited | (1 << i)));
               }
           }
   
           return dp[current][visited] = result;
       }
   }
   
   ```

   <br/>

2. Bit Mask

   > 각 비트는 도시를 의미하고 그에 대한 값으로 방문 여부를 나타내도록
   > 예를 들어, 5개의 도시가 있는 경우 {1, 2, 4} 도시를 방문했다면 이진법으로 11010(2)
   >
   > 이렇게 비트마스킹을 사용하게 되면 공간 복잡성을 크게 줄일 수 있고,
   > 연산 또한 배열을 사용하는 것보다 훨씬 빠르게 수행할 수 있어 시간 복잡도를 개선할 수 있음

```java
public class TravelingSalesman {

    static int N;
    static int[][] world;
    static int[][] dp;

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        N = scanner.nextInt();
        world = new int[N][N];
        dp = new int[N][1 << N];

        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                world[i][j] = scanner.nextInt();
            }
        }

        System.out.println(travelingSalesman(0, 1));
    }

    // 최소 비용을 찾기 위한 재귀 함수
    static int tsp(int now, int visited) {
        // 기저 사례: 모든 도시가 방문되었을 때
        if (visited == (1 << N) - 1) {
            // 가능하다면 시작 도시로 돌아가는 비용을 반환
            return (world[now][0] != 0) ? world[now][0] : (int) 1e9;
        }

        // 현재 상태에 대한 결과가 이미 계산되었다면 반환
        if (dp[now][visited] != 0) {
            return dp[now][visited];
        }

        int minCost = (int) 1e9;

        // 가능한 모든 다음 도시를 반복
        for (int next = 1; next < N; next++) {
            // 도시에 도달할 수 없거나 이미 방문한 경우 건너뛰기
            if (world[now][next] == 0 || (visited & (1 << next)) != 0) {
                continue;
            }

            // 다음 도시의 비용 계산 및 minCost 갱신
            int cost = travelingSalesman(next, visited | (1 << next)) + world[now][next];
            minCost = Math.min(cost, minCost);
        }

        // 결과를 기억하고 최소 비용 반환
        dp[now][visited] = minCost;
        return minCost;
    }
}
```

