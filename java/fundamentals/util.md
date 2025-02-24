# java.util 패키지

**자바에서 가장 많이 사용되는 기본 유틸리티 모음**으로, 자료구조, 날짜/시간, 동시성, 기타 유용한 기능들을 제공



![t](https://scaler.com/topics/images/components-of-java-util-package.webp)

<br/><br/>

#### 1. **컬렉션 프레임워크 (Collection Framework)**

자료구조를 다루는 인터페이스와 클래스를 제공하는 프레임워크이다.

- List (순서 유지, 중복 허용)
  - `ArrayList`, `LinkedList`, `Vector`
- Set (중복 불허, 순서 없음)
  - `HashSet`, `LinkedHashSet`, `TreeSet`
- Map (Key-Value 형태의 자료구조)
  - `HashMap`, `LinkedHashMap`, `TreeMap`
- Queue (FIFO 방식의 자료구조)
  - `LinkedList`, `PriorityQueue`, `ArrayDeque`
- Stack (LIFO 방식의 자료구조)
  - `Stack`

<br/>

#### 2. **날짜 및 시간 처리**

- `Date`, `Calendar` (구버전, Java 8 이전)
- `LocalDate`, `LocalTime`, `LocalDateTime`, `ZonedDateTime` (`java.time` 패키지, Java 8 이후)

<br/>

#### 3. **유틸리티 클래스**

- `Arrays` → 배열 조작(정렬, 검색 등)
- `Collections` → 컬렉션 조작(정렬, 변환 등)
- `Objects` → 객체 유틸리티(Null 체크 등)
- `Optional` → Null 안전성을 높이는 래퍼 클래스

<br/>

#### 4. **동시성 유틸리티**

- `ConcurrentHashMap`, `CopyOnWriteArrayList` (멀티스레드 환경에서 안전한 컬렉션)
- `ExecutorService` (스레드 풀 관리)

<br/>

#### 5. **기타 유틸리티**

- `Random` → 난수 생성
- `Scanner` → 입력 처리
- `Properties` → 설정 파일(.properties) 관리
- `UUID` → 고유 식별자 생성

<br/>

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



<br/><br/>

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





<br/>

참고:

https://www.scaler.com/topics/util-package-in-java/
