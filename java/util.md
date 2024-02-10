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

