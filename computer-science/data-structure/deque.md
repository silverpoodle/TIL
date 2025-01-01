## 덱(Deque)이란?

- 덱(Deque)은 Double-ended Queue의 줄임말로, 양쪽 끝에서 삽입과 삭제가 모두 가능한 자료구조
- 덱은 큐와 스택의 특징을 모두 가지고 있고, 양방향에서 데이터를 처리할 수 있기 때문에 유연하게 활용



## 덱의 구현 방법

덱의 구현 방법은 대표적으로 `배열`을 이용하는 방법과 `연결 리스트`를 이용하는 방법 2가지

1. **배열을 이용한 구현**

   - code

     ```java
     public class ArrayDeque<E> {
         private Object[] elements;
         private int front;
         private int rear;
         private int size;
         private static final int DEFAULT_CAPACITY = 10;
     
         public ArrayDeque() {
             elements = new Object[DEFAULT_CAPACITY];
             front = rear = -1;
             size = 0;
         }
     
         public void addFirst(E element) {
             ensureCapacity();
             if (isEmpty()) {
                 front = rear = 0;
             } else if (front == 0) {
                 // Wrap around to the end of the array
                 front = elements.length - 1;
             } else {
                 front--;
             }
             elements[front] = element;
             size++;
         }
     
         public void addLast(E element) {
             ensureCapacity();
             if (isEmpty()) {
                 front = rear = 0;
             } else if (rear == elements.length - 1) {
                 // Wrap around to the beginning of the array
                 rear = 0;
             } else {
                 rear++;
             }
             elements[rear] = element;
             size++;
         }
     
         public E removeFirst() {
             if (isEmpty()) {
                 throw new IllegalStateException("Deque is empty");
             }
             E removedElement = (E) elements[front];
             if (front == rear) {
                 // Last element is being removed
                 front = rear = -1;
             } else {
                 front = (front + 1) % elements.length;
             }
             size--;
             return removedElement;
         }
     
         public E removeLast() {
             if (isEmpty()) {
                 throw new IllegalStateException("Deque is empty");
             }
             E removedElement = (E) elements[rear];
             if (front == rear) {
                 // Last element is being removed
                 front = rear = -1;
             } else if (rear == 0) {
                 rear = elements.length - 1;
             } else {
                 rear--;
             }
             size--;
             return removedElement;
         }
     
         public E peekFirst() {
             if (isEmpty()) {
                 throw new IllegalStateException("Deque is empty");
             }
             return (E) elements[front];
         }
     
         public E peekLast() {
             if (isEmpty()) {
                 throw new IllegalStateException("Deque is empty");
             }
             return (E) elements[rear];
         }
     
         public int size() {
             return size;
         }
     
         public boolean isEmpty() {
             return size == 0;
         }
     
         private void ensureCapacity() {
             if (size == elements.length) {
                 // Resize the array to twice its current capacity
                 elements = resizeArray(elements, 2 * elements.length);
             }
         }
     
         private Object[] resizeArray(Object[] oldArray, int newSize) {
             Object[] newArray = new Object[newSize];
             int i = 0;
             while (i < size) {
                 newArray[i] = oldArray[(front + i) % oldArray.length];
                 i++;
             }
             front = 0;
             rear = size - 1;
             return newArray;
         }
     
         public static void main(String[] args) {
             ArrayDeque<Integer> deque = new ArrayDeque<>();
             deque.addFirst(1);
             deque.addLast(2);
             deque.addFirst(3);
     
             System.out.println("Size of deque: " + deque.size());
             System.out.println("Front of deque: " + deque.peekFirst());
             System.out.println("Rear of deque: " + deque.peekLast());
     
             System.out.println("Removed element from front: " + deque.removeFirst());
             System.out.println("Removed element from rear: " + deque.removeLast());
     
             System.out.println("Size of deque after removals: " + deque.size());
         }
     }
     ```

2. **연결 리스트를 이용한 구현**

   - code

     ```java
     class Node<E> {
         E data;
         Node<E> prev;
         Node<E> next;
     
         public Node(E data) {
             this.data = data;
             this.prev = null;
             this.next = null;
         }
     }
     
     public class LinkedListDeque<E> {
         private Node<E> front;
         private Node<E> rear;
         private int size;
     
         public LinkedListDeque() {
             this.front = null;
             this.rear = null;
             this.size = 0;
         }
     
         public void addFirst(E element) {
             Node<E> newNode = new Node<>(element);
             if (isEmpty()) {
                 front = rear = newNode;
             } else {
                 newNode.next = front;
                 front.prev = newNode;
                 front = newNode;
             }
             size++;
         }
     
         public void addLast(E element) {
             Node<E> newNode = new Node<>(element);
             if (isEmpty()) {
                 front = rear = newNode;
             } else {
                 rear.next = newNode;
                 newNode.prev = rear;
                 rear = newNode;
             }
             size++;
         }
     
         public E removeFirst() {
             if (isEmpty()) {
                 throw new IllegalStateException("Deque is empty");
             }
             E removedElement = front.data;
             if (front == rear) {
                 // Last element is being removed
                 front = rear = null;
             } else {
                 front = front.next;
                 front.prev = null;
             }
             size--;
             return removedElement;
         }
     
         public E removeLast() {
             if (isEmpty()) {
                 throw new IllegalStateException("Deque is empty");
             }
             E removedElement = rear.data;
             if (front == rear) {
                 // Last element is being removed
                 front = rear = null;
             } else {
                 rear = rear.prev;
                 rear.next = null;
             }
             size--;
             return removedElement;
         }
     
         public E peekFirst() {
             if (isEmpty()) {
                 throw new IllegalStateException("Deque is empty");
             }
             return front.data;
         }
     
         public E peekLast() {
             if (isEmpty()) {
                 throw new IllegalStateException("Deque is empty");
             }
             return rear.data;
         }
     
         public int size() {
             return size;
         }
     
         public boolean isEmpty() {
             return size == 0;
         }
     
         public static void main(String[] args) {
             LinkedListDeque<Integer> deque = new LinkedListDeque<>();
             deque.addFirst(1);
             deque.addLast(2);
             deque.addFirst(3);
     
             System.out.println("Size of deque: " + deque.size());
             System.out.println("Front of deque: " + deque.peekFirst());
             System.out.println("Rear of deque: " + deque.peekLast());
     
             System.out.println("Removed element from front: " + deque.removeFirst());
             System.out.println("Removed element from rear: " + deque.removeLast());
     
             System.out.println("Size of deque after removals: " + deque.size());
         }
     }
     ```





## 덱의 연산

덱에 요소들을 저장/삭제하는 연산, 크기와 현재 상태(비어있는지) 등을 조회

1. `addFirst()` : 덱의 맨 앞에 요소를 저장
2. `addLst()` : 덱의 맨 뒤에 요소를 저장
3. `removeFirst()` : 현재 덱의 맨 앞에 있는 요소를 제거하고 반환
4. `removeLast()` : 현재 덱의 맨 뒤에 있는 요소를 제거하고 반환
5. `peekFirst()` : 현재 덱의 맨 앞에 있는 요소를 반환
6. `peekLast()` : 현재 덱의 맨 뒤에 있는 요소를 반환
7. `isEmpty()` : 현재 덱이 비어있는지 여부를 반환한다. 자바에서는 `boolean` 값으로 반환
8. `size()` : 현재 덱에 저장되어있는 요소의 수를 반환한다. 자바에서는 `int` 값으로 반환





## 덱의 장점과 단점

- 덱은 양쪽 끝에서 삽입과 삭제가 가능한 자료구조로, **큐와 스택의 기능을 모두 수행.** 
- 양쪽에서 효율적으로 데이터를 조작할 수 있어, 다양한 응용 분야에서 유연한 활용이 가능
  -> 큐와 스택을 결합한 형태로 사용하여 **문제에 따라 최적의 연산을 선택**할 수 있다.

- 중간에 있는 **특정 위치의 데이터에 직접 접근하는 데에는 어려움** 
- 덱의 내부 구현에 따라서는 중간 요소에 접근하기 위해선 순차적으로 이동해야 하는 번거로움.
- **다른 자료구조에 비해 구현이 복잡**