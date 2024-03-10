## 1️⃣ 람다 표현식이란?

람다 표현식은 Java 8부터 도입된 기능으로, 함수형 프로그래밍을 구성하는 함수의 표현 방식 중 하나이다. 보통 람다식이라고 한다.

익명 함수를 간결하게 표현하는 방법으로, 함수의 이름을 명시적으로 지정하지 않고 직접 정의하여 사용한다. 이를 통해 메서드를 하나의 식으로 표현할 수 있으며, 클래스를 만들지 않고도 메서드처럼 사용할 수 있다. 메서드의 이름이 필요없기 때문에 익명 함수의 한 종류라고 볼 수 있다. 익명 함수는 모두 일급 객체이고, 일급 객체인 함수는 변수처럼 사용이 가능하며 매개변수로 전달이 가능하다는 특징이 있다.

<br/>

> ❓ **일급 객체**
>
> 일급 객체(First-Class Object)는 다음과 같은 세 가지 특성을 가지는 개체를 가리킨다.
>
> 1. **변수에 할당할 수 있어야한다.** 함수나 변수에 할당이 가능해야 한다. 이는 함수 또는 변수로 객체를 전달하거나 다른 함수에 반환할 수 있음을 의미한다.
> 2. **인자로 전달 가능해야한다.** 함수에 매개변수로 전달할 수 있어야 한다. 다른 함수의 인자로 전달될 수 있어야 한다.
> 3. **반환값으로 사용 가능해야한다.** 함수의 반환값으로 사용될 수 있어야 한다. 다른 함수에서 반환값으로 사용될 수 있어야 한다.
>
> 일급 객체 개념은 특히 함수형 프로그래밍에서 중요한 역할을 한다. 이는 프로그래밍의 유연성을 증가시키고, 추상화 수준을 높여주며, 고차 함수와 같은 강력한 프로그래밍 패턴을 가능하게 한다. 고차 함수는 함수를 인자로 받거나 함수를 결과로 반환하는 함수를 의미한다.

<br/>

람다식은 주로 컬렉션의 반복, 이벤트 처리, 스레드 생성 등에 활용된다. 예를 들어, 컬렉션의 각 요소에 대해 특정 작업을 수행하거나, 스레드를 생성하고 실행하는 등의 작업에 람다식을 활용할 수 있다.

<br/>

## 람다식의 특징

1. **간결성**

   람다식을 사용하면 코드를 더 간결하고 가독성 있게 작성할 수 있다. 특히 반복적인 코드를 줄여주는 데 유용하다.

2. **함수형 프로그래밍 지원**

   람다식은 함수형 인터페이스를 구현할 때 자주 사용된다. 함수형 인터페이스는 하나의 추상 메서드만을 가지고 있으며, 람다식을 통해 해당 메서드의 구현을 제공할 수 있다.

3. **지연 실행**

   람다식을 사용하면 코드를 지연하여 실행할 수 있다. 예를 들어, 스레드를 생성하거나 복잡한 계산을 수행하는 등의 작업을 람다식으로 간단하게 전달할 수 있다.

<br/>

## 람다식의 기본 구문

```java
public int add(int x, int y) {
    return x + y;
}
```

일반 메서드의 경우 접근제한자, 반환 타입, 메서드명, 매개변수, 매개변수 타입, 반환값이 있어야한다.

```java
(int x, int y) -> { return x + y; }
(x, y) -> x + y;
```

람다식의 경우 매개변수를 가진 코드 블록으로 런타임 시에는 익명 구현 객체를 생성하며, 매개변수 , 화살표(→), 바디 이렇게 3가지 부분으로 이루어져있다. 매개변수의 타입도 생략이 가능한데, 컴파일러가 문맥을 통해 변수의 타입을 유추해서 집어넣기 떄문이다. 이를 `타입 추론`이라고 한다.



<br/>

<br/>

## 2️⃣ 함수형 인터페이스

함수형 인터페이스는 Java 8부터 도입된 기능으로, 단 하나의 추상 메서드를 갖는 인터페이스이다. 하나의 추상 메서드만 가져야하는 이유는 람다식은 함수형 인터페이스의 추상 메서드와 1:1로 연결되어야하기 때문이다.

람다식은 이 함수형 인터페이스를 통해 메서드를 직접 구현하거나 전달하는 데 사용된다. 다르게 말하면 아무 클래스나 람다식으로 만드는 것은 안되고, 함수형 인터페이스를 통해 구현한 익명 함수 객체만 람다식으로 만들 수 있다.

자바의 함수형 인터페이스 어노테이션(`@FunctionalInterface`)은 함수를 일급 객체처럼 다룰 수 있게 해주면서, 인터페이스에 선언하여 단 하나의 추상 메서드만은 갖도록 제한하는 역할을 한다. 이 어노테이션을 사용하면 두 개 이상의 메서드 선언 시 컴파일 오류가 발생하게 된다.

<br/>

## 함수형 인터페이스의 조건

1. 단 하나의 추상 메서드를 가져야 한다.
2. default 메서드나 static 메서드는 여러 개 가질 수 있다.
3. `java.lang.Object` ****클래스에서 상속받은 메서드(`equals()`, `hashCode()`, `toString()`)는 계산하지 않는다. 따라서 이 메서드들은 기능 메서드로 취급되지 않는다.

```java
// 함수형 인터페이스 O
@FunctionalInterface
public interface SimpleFunction {
    int apply();
   
    defalt void test() {};
    static void test2() {};
}

// 함수형 인터페이스 X
@FunctionalInterface
public interface NotAFunction {
    void method1();
    void method2();
}
```

<br/>

## 자바에서의 함수형 인터페이스 활용

자바에서는 `java.util.function` 패키지를 통해 다양한 함수형 인터페이스를 제공한다. `Predicate<T>`, `Function<T, R>`, `Consumer<T>`, `Supplier<T>` 등이 있다.예를 들어, `Predicate<T>` 인터페이스는 하나의 인자를 받아 boolean 값을 반환하는 메서드를 가지고 있다. 이를 람다식으로 표현하면 다음과 같다.

```java
Predicate<String> lengthIsGreaterThan5 = str -> str.length() > 5;
```

<br/>

<br/>

## **3️⃣ 람다 표현식 문법**

## **매개변수와 반환 값의 타입 지정**

람다식에서는 매개변수의 타입을 명시적으로 지정할 필요가 없다. 컴파일러가 문맥을 통해 타입을 추론할 수 있기 때문에 생략이 가능하다. 반환 값이 있는 경우에도 `return` 키워드를 사용하지 않고, 표현식 자체가 반환 값으로 처리된다.

```java
// 타입을 명시적으로 지정하는 경우
(int x, int y) -> { return x + y; }

// 매개변수 타입은 자동으로 추론됨
// 반환 값이 있는 경우에도 return 키워드 사용하지 않음
(x, y) -> x + y
```

<br/>

## **중괄호와 return 키워드 사용**

람다식의 바디가 단일 표현식인 경우, 중괄호와 `return` 키워드를 생략할 수 있다. 람다식이 여러 줄로 구성되어 있거나 명시적으로 반환 값이 있을 때는 중괄호 `{}`로 둘러싸고, `return` 키워드를 사용하여 반환 값을 명시해야 한다.

```java
// 중괄호와 return 키워드를 생략하는 경우
(int x, int y) -> x + y;

// 중괄호와 return 키워드를 사용하여 반환 값 명시
(int x, int y) -> {
    int sum = x + y;
    return sum;
}
```

<br/>

## **메서드 레퍼런스와 람다식의 비교**

메서드 레퍼런스는 이미 존재하는 메서드를 호출하는 데 사용된다. 이는 람다식의 축약된 형태로, 더 간결한 코드로 표현된다.

```java
// 람다식
Arrays.sort(strings, (s1, s2) -> s1.compareToIgnoreCase(s2));

// 메서드 레퍼런스
Arrays.sort(strings, String::compareToIgnoreCase);
```

메서드 레퍼런스는 `클래스명::메서드명` 또는 `인스턴스명::메서드명` 형태로 사용된다. 이는 해당 메서드를 직접 호출하는 것이 아니라, 메서드를 참조하여 람다식으로 전달하는 방식이다.

<br/>

### 메서드 레퍼런스 사용법

1. **정적 메서드 참조**

   이 형태는 `클래스명::정적메서드명`으로 사용되며, 특정 클래스의 정적 메서드를 참조한다. 함수형 인터페이스의 메서드와 시그니처가 일치해야 한다. 예를 들어, `Integer::parseInt`는 `Integer` 클래스의 정적 메서드인 `parseInt`를 참조한다.

2. **인스턴스 메서드 참조**

   1. 특정 객체의 인스턴스 메서드

      `인스턴스명::인스턴스메서드명` 형태로 사용되며, 특정 객체의 인스턴스 메서드를 참조한다. 예를 들어, `String myString = "example";`이라는 인스턴스가 있다면, `myString::toUpperCase`는 `myString` 객체의 `toUpperCase` 메서드를 참조한다.

   2. 임의 객체의 인스턴스 메서드

      `클래스명::인스턴스메서드명` 형태로 사용되며, 이는 함수형 인터페이스의 구현에서 첫 번째 매개변수를 메서드의 호출 대상으로 사용한다. 예를 들어, `String::toLowerCase`는 어떤 `String` 객체든 그 객체의 `toLowerCase` 메서드를 참조한다. 이 형태는 특정 객체를 지정하지 않기 때문에, 매개변수로 전달된 객체에 대한 메서드 호출로 이해할 수 있다.

3. **생성자 참조**

   `클래스명::new` 형태로 사용되며, 해당 클래스의 생성자를 참조한다. 예를 들어, `ArrayList::new`는 `ArrayList`의 새 인스턴스를 생성한다.



<br/>

<br/>

## 4️⃣ 람다 표현식의 활용

## 컬렉션 요소의 순회

기존의 for-loop나 iterator를 사용하는 대신, `forEach` 메서드를 사용하여 람다식으로 각 요소에 대한 작업을 정의할 수 있다. `forEach` 메서드는 `Iterable` 인터페이스에 정의되어 있으며, 이 메서드는 `Consumer` 타입의 매개변수를 받는다. `Consumer` 인터페이스는 자바의 함수형 인터페이스 중 하나로, 입력을 받고 반환값은 없는 연산을 수행한다.

```java
List<String> fruits = Arrays.asList("사과", "바나나", "체리");
fruits.forEach(fruit -> System.out.println(fruit));
```

위 코드에서 `name -> System.out.println(name)` 부분은 `Consumer` 인터페이스의 반환값이 없는 `accept` 메서드를 구현한 람다식이다.

<br/>

## 함수형 인터페이스를 매개변수로 받는 메서드 사용

람다식을 함수형 인터페이스를 매개변수로 받는 메서드에 전달하여 사용할 수 있다. 예를 들어, 정렬, 스레드 실행, 이벤트 처리 등에 람다식을 사용할 수 있다.

```java
List<Integer> numbers = Arrays.asList(3, 1, 4, 1, 5, 9);
Collections.sort(numbers, (a, b) -> a.compareTo(b));
```

여기서 `(a, b) -> a.compareTo(b)`는 `Comparator` 인터페이스의 구현체를 람다식으로 제공한 것이다. 이는 두 객체 a와 b를 비교하여 정렬 기준을 정의한다.

<br/>

## 스트림 API와의 조합

스트림 API는 Java 8에서 도입된 기능으로, 컬렉션의 요소를 파이프라인 방식으로 처리할 수 있게 해준다. 람다식과 스트림 API를 결합하면, 데이터를 선언적으로 처리할 수 있어 코드가 매우 간결해진다.

```java
List<String> names = Arrays.asList("김철수", "이영희", "박영수", "최영희");
List<String> filteredNames = names.stream()
                                   .filter(name -> name.contains("영"))
                                   .collect(Collectors.toList());
```

위 코드에서 `filter` 메서드는 조건에 맞는 요소만을 선택하는 중간 연산이며, `collect` 메서드는 결과를 리스트로 수집하는 최종 연산이다. `name -> name.contains("영")` 람다식은 "영"을 포함하는 이름만 필터링하는 기준을 정의한다.

<br/>

<br/>

## 5️⃣ 람다 표현식의 예외 처리

람다식의 예외 처리는 내부에서도 처리할 수 있지만, 가능하면 외부에서 처리하는 것이 권장된다.

1. **단순성 유지**

   람다식은 간결하고 명확한 함수형 프로그래밍을 지원하기 위해 도입되었다. 이러한 설계 목적상, 람다식 내부에서 복잡한 예외 처리 로직을 구현하는 것은 권장되지 않는다.

2. **재사용성 향상**

   람다식을 재사용하기 위해서는, 해당 람다식이 특정 상황에만 구속되지 않고 다양한 상황에서 유연하게 사용될 수 있어야 한다. 예외 처리 로직을 람다식 내부에 포함시키면, 그 람다식은 특정 예외 상황에만 적용될 수 있어, 재사용성이 저하된다.

3. **책임의 분리**

   함수형 프로그래밍에서는 작업을 작은 함수 단위로 분리하는 것을 권장한다. 각 함수는 하나의 역할만 수행해야 한다. 예외 처리는 그 자체로 하나의 중요한 역할이며, 때로는 별도의 처리 로직을 요구한다. 따라서, 예외 처리를 람다식 내부에서 처리하는 것은 책임 분리 측면에서 바람직하지 못하다.

<br/>

## try-catch 블록 사용

람다식 내부에서 직접 예외를 처리하는 방법이다. 위에서 말했듯이 권장되는 방법은 아니다.

```java
public class Main {
    public static void main(String[] args) {
        // 람다식 내부에서 예외 발생
        Runnable runnable = () -> {
            try {
                int result = 10 / 0; // ArithmeticException 발생
                System.out.println("Result: " + result);
            } catch (ArithmeticException e) {
                System.out.println("Caught exception: " + e.getMessage());
            }
        };
        
        // 람다식 실행
        runnable.run();
    }
}
```

<br/>

## 예외 전파

람다식 내부에서 발생한 예외를 호출자에게 전파하여 호출자에서 예외를 처리하도록 할 수 있다. 이 경우에는 람다식의 시그니처에 throws 절을 추가하여 해당 예외를 호출자에게 알려준다. 호출자는 해당 예외를 처리하는 catch 블록을 사용하여 예외를 처리할 수 있다. 람다식 내부에서 예외 처리를 강제하지 않고, 호출자에게 예외 처리의 책임을 넘기는 것이다.

```java
public class Main {
    public static void main(String[] args) {
        // 람다식에서 예외 전파
        Runnable runnable = () -> {
            int result = 10 / 0; // ArithmeticException 발생
            System.out.println("Result: " + result);
        };

        // 람다식 실행
        try {
            runnable.run();
        } catch (ArithmeticException e) {
            System.out.println("Caught exception: " + e.getMessage());
        }
    }
}
```

<br/>

## 예외를 래핑하는 래퍼 메서드 사용

람다식에서 체크 예외(Checked Exception)를 처리해야 할 때, Java의 람다식은 체크 예외를 직접 던질 수 없다. 이 문제를 해결하기 위해, 예외를 Runtime Exception으로 래핑하는 래퍼 메서드를 사용할 수 있다.

```java
@FunctionalInterface
public interface ThrowingConsumer<T, E extends Exception> {
    void accept(T t) throws E;
}

public static <T> Consumer<T> wrap(ThrowingConsumer<T, Exception> throwingConsumer) {
    return i -> {
        try {
            throwingConsumer.accept(i);
        } catch (Exception e) {
            throw new RuntimeException(e);
        }
    };
}

// 사용 예
Stream.of("a", "b", "c")
      .forEach(wrap(s -> {
          // 체크 예외를 발생시킬 수 있는 코드
      }));
```

<br/>

## 함수형 인터페이스 내부에서 예외 처리

함수형 인터페이스의 메서드에 throws 절을 추가하여 예외를 처리할 수 있다. 이때 함수형 인터페이스를 사용하는 코드에서 해당 예외를 처리하거나 예외를 던질 수 있다. 함수형 인터페이스를 구현하는 클래스에서 예외 처리를 강제하고, 함수형 인터페이스를 사용하는 코드에서 해당 예외를 처리하도록 하는 것이다.

```java
@FunctionalInterface
interface MyFunctionalInterface {
    void myMethod() throws Exception; // 예외 처리를 요구하는 함수형 인터페이스
}

public class Main {
    public static void main(String[] args) {
        // 함수형 인터페이스 구현
        MyFunctionalInterface myFunctionalInterface = () -> {
            int result = 10 / 0; // ArithmeticException 발생
            System.out.println("Result: " + result);
        };

        // 람다식 실행
        try {
            myFunctionalInterface.myMethod();
        } catch (ArithmeticException e) {
            System.out.println("Caught exception: " + e.getMessage());
        } catch (Exception e) {
            System.out.println("Caught exception: " + e.getMessage());
        }
    }
}
```

<br/>

<br/>



## 6️⃣ 람다 표현식의 제약

## 람다식의 제약 사항

1. **타입 추론의 한계**

   람다식은 컴파일러에 의한 타입 추론을 기반으로 작동한다. 때때로 컴파일러가 람다식의 파라미터 타입을 명확하게 추론하지 못하고, 컴파일 에러가 발생하는 경우가 있다. 이런 상황에서는 타입을 명시적으로 지정해줘야 한다.

2. **지역 변수에 대한 제약**

   람다식 내에서 사용되는 지역 변수는 final 이거나 사실상 final(effective final)이어야 한다. 즉, 람다식이 실행되는 동안 지역 변수에 대한 변경을 허용하지 않는다. 그렇지않으면 컴파일 에러가 발생한다.

3. **문서화 불가능**

   람다식은 이름 없는 함수이기 때문에 메서드나 클래스와 다르게 문서화 할 수 없다.

4. **디버깅 어려움**

   람다식은 코드 내부에 이름이 없는 익명 함수로 존재하기 때문에, 스택 추적 정보가 제한되거나 람다식의 내용이 복잡한 경우 디버깅하기 어려울 수 있다.

5. **직렬화 문제**

   람다식은 내부적으로 익명 클래스로 구현되기 때문에 직렬화하기 어렵다. 람다식을 포함한 클래스를 직렬화하려면 해당 클래스의 인스턴스 변수와 상태를 저장해야 한다. 그러나 람다식은 익명 클래스로 구현되어 있어서 직렬화하는 데 필요한 정보가 부족할 수 있다. 람다식을 사용하는 클래스의 인스턴스를 직렬화하려고 하면 런타임 시 직렬화 오류가 발생할 수 있다.



### 참고

[[Java\] 람다식(Lambda Expression)과 함수형 인터페이스(Functional Interface) - (2/5)](https://mangkyu.tistory.com/113)

[☕ 람다 표현식(Lambda Expression) 완벽 정리](https://inpa.tistory.com/entry/☕-Lambda-Expression)

[[Java\]람다 표현식에서 Unchecked Exception 처리](https://developer-talk.tistory.com/840)