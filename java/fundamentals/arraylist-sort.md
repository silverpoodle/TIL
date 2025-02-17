# Sort ArrayList

Java 에서 자주 사용되는 자료구조인 `ArrayList`

ArrayList 내부의 데이터들을 정렬하는 방법을 알아보쟈 😋

<img src="https://www.scaler.com/topics/images/how-to-sort-arrayList-in-java-thumbnail.webp" alt="ㅁ" style="zoom:50%;" />

<br/>

## 1. Collections.sort()

```java
import java.util.ArrayList;
import java.util.Collections;

public class Main {
    public static void main(String[] args) {
        ArrayList<String> list1 = new ArrayList<>(Arrays.asList(1, 2, 3, 4, 5));
        ArrayList<String> list2 = new ArrayList<>(Arrays.asList("C", "A", "B", "a"));

        Collections.sort(list1);  // 오름차순 정렬
        Collections.sort(list2);  // 오름차순 정렬
        Collections.sort(list1, Collections.reverseOrder());  // 내림차순 정렬
        Collections.sort(list2, String.CASE_INSENSITIVE_ORDER); // 대소문자 구분없이 오름차순
        Collections.sort(list, Collections.reverseOrder(String.CASE_INSENSITIVE_ORDER)); // 대소문자 구분없이 내림차순
    }
}
```

<br/><br/>



<br/><br/>

## 2. List.sort()

```java
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Comparator; 
public class SortArrayList {    
  public static void main(String[] args) {       
    ArrayList<String> list = new ArrayList<>(Arrays.asList("C", "A", "B", "a"));            
    
    list.sort(Comparator.naturalOrder()); // 오름차순  
    list.sort(Comparator.reverseOrder()); // 내림차순
    list.sort(String.CASE_INSENSITIVE_ORDER); // 대소문자 구분 없이 오름차순 
    list.sort(Collections.reverseOrder(String.CASE_INSENSITIVE_ORDER)); //대소문자 구분 없이 내림차순    
  }
}
```

<br/>

### 💡Collections 와 List sort 차이

### 1. **정렬 메서드가 속한 클래스**

- `Collections.sort(List<T> list)`: `java.util.Collections` 클래스에 속한 정적(static) 메서드
- `List.sort(Comparator<? super T> c)`: `java.util.List` 인터페이스의 디폴트 메서드(default method)

### 2. **호출 방식**

- `Collections.sort(list);` → `Collections` 클래스의 정적 메서드를 사용하여 정렬
- `list.sort(comparator);` → `List` 인터페이스의 인스턴스 메서드를 사용하여 정렬

### 3. **Comparator 인자**

- `Collections.sort(List<T> list)`는 내부적으로 `Collections.sort(list, null);`과 같으며, `null`이 전달되면 리스트의 요소가 `Comparable<T>`을 구현해야 함
- `List.sort(Comparator<? super T> c)`는 반드시 `Comparator`를 인자로 받으며, `null`을 전달하면 `Comparable`을 기준으로 정렬

### 4. **사용하는 정렬 알고리즘**

- 두 메서드는 동일한 내부 정렬 알고리즘(`TimSort`)을 사용
- `Collections.sort()`는 내부적으로 `List.sort()`를 호출하여 동작

<br/>

| 차이점               | `Collections.sort()`                | `List.sort()`                       |
| -------------------- | ----------------------------------- | ----------------------------------- |
| 소속 클래스          | `Collections`                       | `List` (default method)             |
| 호출 방식            | `Collections.sort(list)`            | `list.sort(comparator)`             |
| Comparator 필요 여부 | 선택 (null 시 `Comparable<T>` 사용) | 필요 (null 시 `Comparable<T>` 사용) |
| 내부 구현            | `list.sort(comparator)` 호출        | 직접 정렬                           |
| 도입 버전            | Java 2 (JDK 1.2)                    | Java 8                              |

📌 **결론:** `List.sort()`는 `Collections.sort()`의 최신 대체 방식이며, 더 직관적이고 객체지향적 🚀

<br/><br/>

## 3. 사용자 정의 정렬 - Comparator 사용

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.Comparator;

class Person {
    String name;
    int age;
    
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    @Override
    public String toString() {
        return name + "(" + age + ")";
    }
}

public class Main {
    public static void main(String[] args) {
        ArrayList<Person> people = new ArrayList<>();
        people.add(new Person("Alice", 30));
        people.add(new Person("Bob", 25));
        people.add(new Person("Charlie", 35));
        
        
        // 나이 기준 오름차순 정렬
        Collections.sort(people, new Comparator<Person>() {
            @Override
            public int compare(Person p1, Person p2) {
                return Integer.compare(p1.age, p2.age);
            }
        });
        
    }
}
```



<br/><br/>

## 4. 람다식을 이용한 정렬

Java 8부터는 `Comparator`를 람다식으로 간단하게 표현

```java
Collections.sort(people, (p1, p2) -> Integer.compare(p1.age, p2.age));
```

또는 `List.sort()`를 사용

```java
people.sort(Comparator.comparingInt(p -> p.age));
```



<br/><br/>

## 5. 정렬 시 주의할 점

- `Collections.sort()`는 `O(n log n)`의 시간 복잡도
- `null` 값이 포함된 경우 `NullPointerException`이 발생
- `Comparable` 인터페이스를 구현하여 `compareTo()` 메서드를 정의하면 기본 정렬 기준을 설정 가능

```java
class Person implements Comparable<Person> {
    String name;
    int age;
    
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
    
    @Override
    public int compareTo(Person other) {
        return Integer.compare(this.age, other.age);
    }
}
```

