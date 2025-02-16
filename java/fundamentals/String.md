# String in Java

## 1. String의 특징

- **불변(Immutable) 객체**: 한 번 생성되면 그 값을 변경할 수 없음. 값을 변경하려면 새로운 객체를 생성!

  ```java
  String str = "Hello";
  str = str + " World"; // 새로운 String 객체 생성
  ```

- **String Pool**: 자주 사용되는 문자열 리터럴을 효율적으로 관리하기 위해 JVM은 **String Pool**을 제공
  동일한 값을 가진 문자열 리터럴은 **String Pool**에 저장되고, 동일한 값을 참조하도록 설계됩니다.

  ```java
  String str1 = "Hello";
  String str2 = "Hello";
  System.out.println(str1 == str2); // true (같은 객체 참조)
  ```

<br/><br/>

## 2. String 객체 생성 방법

- 리터럴(Literal) 방식 : String Pool에서 관리

```java
String str = "Hello";
```

- new 키워드로 생성: 새로운 객체를 힙 메모리에 생성

```java
String str = new String("Hello");
```

<br/><br/>

## 3. String 주요 메서드

- 문자열 길이 확인

  ```java
  String str = "Hello";
  System.out.println(str.length()); // 5
  ```

- 문자 접근

  ```java
  System.out.println(str.charAt(1)); // 'e'
  ```

- 부분 문자열 추출

  ```java
  String str = "Hello, World!";
  System.out.println(str.substring(0, 5)); // "Hello"
  ```

- 문자열 비교

  ```java
  String str1 = "hello";
  String str2 = "Hello";
  System.out.println(str1.equals(str2)); // false
  System.out.println(str1.equalsIgnoreCase(str2)); // true
  ```

- 문자열 검색

  ```java
  String str = "Hello, World!";
  System.out.println(str.indexOf("World")); // 7
  System.out.println(str.lastIndexOf("o")); // 8
  ```

- 문자열 치환

  ```java
  String str = "Hello, World!";
  System.out.println(str.replace("World", "Java")); // "Hello, Java!"
  ```

- 문자열 분리

  ```java
  String str = "apple,banana,cherry";
  String[] fruits = str.split(",");
  for (String fruit : fruits) {
      System.out.println(fruit);
  }
  ```

- 대소문자 변환

  ```java
  String str = "Hello";
  System.out.println(str.toUpperCase()); // "HELLO"
  System.out.println(str.toLowerCase()); // "hello"
  ```

- 공백 제거

  ```java
  String str = "   Hello   ";
  System.out.println(str.trim()); // "Hello"
  ```

<br/><br/>

## 4. String의 효율적 사용

- 문자열을 자주 변경해야 하는 경우 ***StringBuilder 또는 StringBuffer*** 사용! 

  ```java
  // 둘은 가변(Mutable) 객체로, 문자열 변경 작업에서 더 높은 성능
  StringBuilder sb = new StringBuilder("Hello");
  sb.append(" World");
  System.out.println(sb.toString()); // "Hello World"
  ```

<br/>

| 특징              | String      | StringBuilder        | StringBuffer              |
| ----------------- | ----------- | -------------------- | ------------------------- |
| **불변성**        | 불변        | 가변                 | 가변                      |
| **스레드 안전성** | 스레드 안전 | 스레드 안전하지 않음 | 스레드 안전               |
| **속도**          | 느림        | 빠름                 | 느림 (동기화 때문에 느림) |

<br/><br/>

## 5. isEmpty? isBlank?

```java
//러하러하
public void checkPostValidation(String content) {
    if (content.isEmpty()) {
        log.warn("게시글 내용 1글자 이하");
        throw new IllegalArgumentException("내용은 1글자 이상이어야 합니다.");
    }
    if (content.isBlank()) {
        log.warn("게시글 내용 1글자 이하");
        throw new IllegalArgumentException("내용은 1글자 이상이어야 합니다.");
    }

}
```

- 🤔둘이 모가 다른가요🤔

  - `isEmpty()`: 문자열의 **길이가  0** 인지 확인, 공백 문자는 포함 ❌

    ```java
    String str = "";
    System.out.println(str.isEmpty()); // true
    
    String str = " ";
    System.out.println(str.isEmpty()); // false
    ```

  - `isBlank()`: 문자열이 **공백 문자로만** 구성되었는지를 확인

    ```java
    String str = "";
    System.out.println(str.isBlank()); // true
    
    String str2 = " ";
    System.out.println(str2.isBlank()); // true
    
    String str3 = "\t\n";
    System.out.println(str3.isBlank()); // true
    ```

    

