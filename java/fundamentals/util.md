### java.util.Stack

```java
import java.util.Stack; //import

Stack<Integer> stack = new Stack<>(); //int형 스택 선언
Stack<String> stack = new Stack<>(); //string 형 스택 선언
Stack<Character> stack = new Stack<>(); //char 형 스택 선언

stack.push(1);     // stack에 값 1 추가
stack.push(2);     // stack에 값 2 추가
stack.pop();       // stack에 값 제거
stack.clear();     // stack의 전체 값 제거 (초기화)
stack.peek();     // stack의 가장 상단의 값 출력

stack.size();      // stack의 크기 출력
stack.empty();     // stack이 비어있는제 check (비어있다면 true)
stack.contains(1) // stack에 1이 있는지 check (있다면 true)
```



#### java.util.Queue

```java
import java.util.LinkedList; //Queue 인터페이스는 주로 LinkedList 클래스에 의해 구현
import java.util.Queue;

Queue<Integer> queue = new LinkedList<>(); // int형 큐 선언
Queue<String> queue = new LinkedList<>(); // string 형 큐 선언
Queue<Character> queue = new LinkedList<>(); // char 형 큐 선언

queue.offer(1);     // queue에 값 1 추가
queue.offer(2);     // queue에 값 2 추가
queue.poll();       // queue에서 값 제거
queue.clear();      // queue의 전체 값 제거 (초기화)
queue.peek();       // queue의 가장 앞의 값 출력

queue.size();       // queue의 크기 출력
queue.isEmpty();    // queue가 비어있는지 확인 (비어있다면 true)
queue.contains(1);  // queue에 1이 있는지 확인 (있다면 true)

```

