# HashSet



<img src="https://cdn.codegym.cc/images/article/ea2c7542-7ffe-44c0-8d89-701d5573f33b/512.webp" alt="f" style="zoom:60%;" />

<br/>

## 1. 구조

- HashSet은 내부적으로 HashMap을 사용하여 데이터를 저장
- 요소들은 해시 테이블에 저장되며, 각 요소의 해시 코드를 이용하여 해당 요소를 찾음

<img src="https://miro.medium.com/v2/resize:fit:786/format:webp/1*hZwONxyDuREb4XqrxYflDA.png" alt="ㅇㅇ" style="zoom:80%;" />



<br/><br/>

## 2. 특징

- 중복 요소 ❌
- 요소의 순서를 보장 ❌
- null 값을 **하나만** 저장
- 동기화❌, 멀티스레드 환경에서는 주의
- 해시 함수를 사용하므로 검색, 삽입, 삭제 연산의 시간 복잡도가 일반적으로 **`O(1)`**



<br/><br/>

## 3. 예시 코드(Java)

```java
import java.util.HashSet;

public class HashSetExample {
    public static void main(String[] args) {
        // HashSet 생성
        HashSet<String> fruits = new HashSet<>();
        
        // 요소 추가
        fruits.add("사과");
        fruits.add("바나나");
        fruits.add("오렌지");
        fruits.add("사과");  // 중복 요소는 추가되지 않음
        
        // HashSet 내용 출력
        System.out.println("과일 목록: " + fruits);
        
        // 요소 포함 여부 확인
        System.out.println("'사과' 포함 여부: " + fruits.contains("사과"));
        
        // 요소 삭제
        fruits.remove("바나나");
        System.out.println("바나나 삭제 후: " + fruits);
        
        // 모든 요소 순회
        System.out.println("모든 과일 순회:");
        for (String fruit : fruits) {
            System.out.println(fruit);
        }
        
        // HashSet 크기
        System.out.println("HashSet 크기: " + fruits.size());
        
        // HashSet 비우기
        fruits.clear();
        System.out.println("HashSet 비운 후 크기: " + fruits.size());
    }
}
```

<br/><br/>

## 4. 자주 쓰이는 메소드

- `add(E e)`: 지정된 요소를 HashSet에 추가
- `remove(Object o)`: 지정된 요소를 HashSet에서 제거
- `contains(Object o)`: HashSet에 지정된 요소가 있는지 확인
- `size()`: HashSet의 요소 개수 반환
- `isEmpty()`: HashSet이 비어있는지 확인
- `clear()`: HashSet의 모든 요소 제거
- `iterator()`: HashSet의 요소를 순회하는 Iterator 반환
- `addAll(Collection<? extends E> c)`: 지정된 컬렉션의 모든 요소를 HashSet에 추가
- `removeAll(Collection<?> c)`: 지정된 컬렉션의 요소와 일치하는 모든 요소를 HashSet에서 제거
- `retainAll(Collection<?> c)`: 지정된 컬렉션의 요소만 HashSet에 남기고 나머지 제거

<br/><br/>



## 5. Set과 비교

<img src="https://www.learnerslesson.com/JAVA/Images/Set.png" alt="dd" style="zoom:60%;" />



HashSet은 Set 인터페이스의 구현체이며, 다른 Set 구현체와 비교하면:

- **HashSet**: 순서를 보장하지 않지만 가장 빠른 검색, 삽입, 삭제 성능
- **LinkedHashSet**: 삽입 순서를 유지하면서 HashSet의 기능 제공
- **TreeSet**: 요소를 자연 순서나 지정된 Comparator에 따라 정렬된 상태로 유지, 이진 검색 트리(Red-Black Tree) 기반

<br/><br/>

참고:

https://velog.io/@acacia__u/hashSet

https://javatutorial.net/java-hashset-example/

https://www.geeksforgeeks.org/hashset-in-java/

https://www.learnerslesson.com/JAVA/Java-HashSet.htm

https://medium.com/javarevisited/internal-working-of-hashset-in-java-interview-question-129bdd31fc60