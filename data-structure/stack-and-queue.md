## 스택(Stack)이란?

<img src="https://blog.kakaocdn.net/dn/b1j1EP/btrAcWiIeeQ/PAUT9taBoi7hkhJh4O5160/img.png" alt="스택의 구조" style="zoom:80%;" />

**스택(Stack)**은 후입선출(Last In - First Out, LIFO)의 구조.
이는 가장 최근에 들어온 데이터가 가장 먼저 나가는 구조로, 데이터는 한 방향으로만 넣고 뺼 수 있다. 

활용예시

- 방문기록
- 실행취소
- 후위 표기법 계산



## 스택의 구현 방법

스택의 구현 방법은 대표적으로 `배열`을 이용하는 방법과 `연결 리스트`를 이용하는 방법 2가지가 있다.

1. **배열을 이용한 구현**

   - code

     ```java
     public class ArrayStack {
         private int maxSize;
         private int top;
         private int[] stackArray;
     
         public ArrayStack(int size) {
             maxSize = size;
             stackArray = new int[maxSize];
             top = -1; // 초기에는 스택이 비어있음을 나타내기 위해 -1로 설정
         }
     
         public void push(int value) {
             if (top < maxSize - 1) {
                 stackArray[++top] = value;
             } else {
                 System.out.println("스택이 가득 찼습니다.");
             }
         }
     
         public int pop() {
             if (top >= 0) {
                 return stackArray[top--];
             } else {
                 System.out.println("스택이 비어있습니다.");
                 return -1; // 스택이 비어있을 때의 특별한 값 또는 예외 처리를 수행할 수 있음
             }
         }
     
         public int peek() {
             if (top >= 0) {
                 return stackArray[top];
             } else {
                 System.out.println("스택이 비어있습니다.");
                 return -1;
             }
         }
     
         public boolean isEmpty() {
             return top == -1;
         }
     
         public int size() {
             return top + 1;
         }
     }
     ```

2. **연결 리스트를 이용한 구현**

   - code

     ```java
     public class Node {
         public int data;
         public Node next;
     
         public Node(int data) {
             this.data = data;
             this.next = null;
         }
     }
     
     public class LinkedStack {
         private Node top;
     
         public LinkedStack() {
             this.top = null;
         }
     
         public void push(int value) {
             Node newNode = new Node(value);
             if (top == null) {
                 top = newNode;
             } else {
                 newNode.next = top;
                 top = newNode;
             }
         }
     
         public int pop() {
             if (top != null) {
                 int value = top.data;
                 top = top.next;
                 return value;
             } else {
                 System.out.println("스택이 비어있습니다.");
                 return -1;
             }
         }
     
         public int peek() {
             if (top != null) {
                 return top.data;
             } else {
                 System.out.println("스택이 비어있습니다.");
                 return -1;
             }
         }
     
         public boolean isEmpty() {
             return top == null;
         }
     
         public int size() {
             int count = 0;
             Node current = top;
             while (current != null) {
                 count++;
                 current = current.next;
             }
             return count;
         }
     }
     ```





## 스택의 연산

스택에 요소들을 저장/삭제하는 연산, 크기와 현재 상태(비어있는지) 등을 조회

1. `push()` : 스택에 요소를 저장
2. `pop()` : 현재 스택의 맨 위에 있는 요소를 제거하고 값을 반환
3. `peek()` : 현재 스택의 맨 위에 있는 요소를 반환. pop()과 다르게 제거하지는 않음
4. `isEmpty()` : 현재 스택이 비어있는지 여부를 반환. 자바에서는 `boolean` 값으로 반환
5. `size()` : 현재 스택에 저장되어있는 요소의 수를 반환. 자바에서는 `int` 값으로 반환





## 스택의 장점과 단점

- 스택은 데이터를 후입선출(LIFO)의 순서로 처리하여 **구현이 간단하고 효율적**
- **메모리 할당 및 해제에 대한 오버헤드가 적어** 자원 관리에 효율적으로 사용.
-  함수 호출 시 지역 변수와 함수 호출 정보를 스택에 저장하여 재귀적인 구조를 간단히 처리

- **중간에 있는 데이터에 직접 접근하는 것이 어려우며**, 특정 위치의 데이터를 삭제하려면 맨 위부터 순차적으로, 모든 데이터를 제거.
- **추가적인 연산을 필요**로 하므로 성능 저하의 가능성





## 큐(Queue)란?

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/52/Data_Queue.svg/220px-Data_Queue.svg.png" alt="img" style="zoom:150%;" />

**큐(Queue)**는 선입선출(First In - First Out, FIFO)의 구조를 가진 자료구조
이는 가장 먼저 추가된 요소가 가장 먼저 제거되는 구조로, 한 방향으로 데이터가 들어가면 다른 방향으로 데이터가 나가는 구조. 

활용예시

- 은행 업무
- 콜센터 고객 대기시간
- BFS
- 캐시 구현



## 큐의 구현 방법

큐의 구현 방법은 대표적으로 `배열`을 이용하는 방법과 `연결 리스트`를 이용하는 방법 2가지

1. **배열을 이용한 구현**

   - code

     ```java
     public class ArrayQueue {
         private static final int MAX_SIZE = 100;
         private int[] queueArray;
         private int front, rear;
     
         public ArrayQueue() {
             this.queueArray = new int[MAX_SIZE];
             this.front = -1;
             this.rear = -1;
         }
     
         public void enqueue(int data) {
             if (rear == MAX_SIZE - 1) {
                 System.out.println("큐가 가득 찼습니다.");
                 return;
             }
             if (front == -1) {
                 front++;
             }
             queueArray[++rear] = data;
         }
     
         public int dequeue() {
             if (front == -1 || front > rear) {
                 System.out.println("큐가 비어있습니다.");
                 return -1; // 또는 예외 처리
             }
             return queueArray[front++];
         }
     
         public int peek() {
             if (front == -1 || front > rear) {
                 System.out.println("큐가 비어있습니다.");
                 return -1; // 또는 예외 처리
             }
             return queueArray[front];
         }
     
         public boolean isEmpty() {
             return front == -1 || front > rear;
         }
     
         public int size() {
             return isEmpty() ? 0 : rear - front + 1;
         }
     }
     ```

2. **연결 리스트를 이용한 구현**

   - code

     ```java
     class Node {
         int data;
         Node next;
     
         public Node(int data) {
             this.data = data;
             this.next = null;
         }
     }
     
     public class LinkedQueue {
         private Node front, rear;
     
         public LinkedQueue() {
             this.front = this.rear = null;
         }
     
         public void enqueue(int data) {
             Node newNode = new Node(data);
             if (rear == null) {
                 front = rear = newNode;
                 return;
             }
             rear.next = newNode;
             rear = newNode;
         }
     
         public int dequeue() {
             if (front == null) {
                 System.out.println("큐가 비어있습니다.");
                 return -1; // 또는 예외 처리
             }
             int data = front.data;
             front = front.next;
             if (front == null) {
                 rear = null;
             }
             return data;
         }
     
         public int peek() {
             if (front == null) {
                 System.out.println("큐가 비어있습니다.");
                 return -1; // 또는 예외 처리
             }
             return front.data;
         }
     
         public boolean isEmpty() {
             return front == null;
         }
     
         public int size() {
             int count = 0;
             Node current = front;
             while (current != null) {
                 count++;
                 current = current.next;
             }
             return count;
         }
     }
     ```



## 큐의 연산

큐에 요소들을 저장/삭제하는 연산, 크기와 현재 상태(비어있는지) 등을 조회하는 연산들
peek(), poll(), remove()는 모두 맨 앞에 있는 요소를 반환하는 메서드
하지만 값을 큐에서 제거하는지, 큐가 비어 있을 때 null을 반환하는지, Exception을 반환하는지 등의 차이가 있기 때문에 사용에 주의

1. `offer()` : 큐에 요소를 저장
2. `peek()` : 현재 큐의 맨 앞에 있는 요소를 반환한다**.** 큐가 비어있으면 `null`을 반환
3. `poll()` : 현재 큐의 맨 앞에 있는 요소를 큐에서 제거하고 값을 반환한다. 큐가 비어있으면 `null`을 반환
4. `remove()` : 현재 큐의 맨 앞에 있는 요소를 큐에서 제거하고 값을 반환한다. 큐가 비어있으면 `NoSuchElementException`이 발생
5. `isEmpty()` : 현재 큐가 비어있는지 여부를 반환한다. 자바에서는 `boolean` 값으로 반환
6. `size()` : 현재 큐에 저장되어있는 요소의 수를 반환한다. 자바에서는 `int` 값으로 반환



## 큐의 장점과 단점

- 큐는 선입선출(FIFO)의 원칙을 따르므로 **데이터 처리가 순차적이고 예측 가능**
- 작업이나 이벤트를 **순서대로 처리해야 하는 상황에서 유용**하며, 멀티스레드 환경에서 동기화된 데이터 전달에 활용

- **특정 위치의 데이터를 삭제하거나 업데이트하는 데 비효율적일 수 있다.** 
- 데이터를 **삭제할 때마다 나머지 데이터들이 한 칸씩 이동해야 하는 비용이 발생**하며, 크기가 클수록 이동 비용이 증가하여 성능에 영향