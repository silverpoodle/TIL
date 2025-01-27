# Test Exceptions in Spring

<img src="https://media.geeksforgeeks.org/wp-content/uploads/20230613122108/Exception-Handling-768.png" alt="ㅇ" style="zoom:67%;" />

<br/>

## 1. JUnit5의 예외 테스트

### 1.1. assertThrows()

- 특정 예외 타입 **또는 그 하위 타입** 이 발생하는지 확인

  ```java
  static <T extends Throwable> T assertThrows(Class<T> expectedType, Executable executable)
  static <T extends Throwable> T assertThrows(Class<T> expectedType, Executable executable, String message)
  static <T extends Throwable> T assertThrows(Class<T> expectedType, Executable executable, Supplier<String> messageSupplier)
  ```

- EX.

  ```java
  @Test
  void testExpectedException() {
      RuntimeException thrown = Assertions.assertThrows(RuntimeException.class, () -> {
          throw new IllegalArgumentException("custom error message");
      });
      assertEquals("custom error message", thrown.getMessage());
  }
  ```



<br/>

### 1.2. assertThrowsExactly()

- 특정 예외 타입만 허용하며, 하위 타입은 허용하지 않음

- EX.

  ```java
  @Test
  void testExpectedExceptionWithExactType() {
      assertThrowsExactly(IllegalArgumentException.class, () -> {
          throw new IllegalArgumentException("exact error message");
      });
  }
  ```

<br/>

### 1.3. assertDoesNotThrow()

- 코드 블록에서 예외가 발생하지 않는지 확인

- EX.

  ```java
  @Test
  void testDoesNotThrowException() {
      Assertions.assertDoesNotThrow(() -> {
          // 예외처리 되지 않는 코드
      });
  }
  ```

<br/><br/>



## 2. AssertJ의 예외 테스트

### 2.1. assertThatThrownBy()

- 체이닝을 통해 **가독성**이 높아짐

- 예외 타입 및 메시지를 직관적으로 검증

- EX.

  ```java
  import static org.assertj.core.api.Assertions.assertThatThrownBy;
  
  @Test
  void testExceptionWithAssertJ() {
      assertThatThrownBy(() -> {
          throw new IllegalArgumentException("error message");
      })
      .isInstanceOf(IllegalArgumentException.class)
      .hasMessage("error message");
  }
  ```



<br/>

<br/>

참고

https://covenant.tistory.com/256

https://howtodoinjava.com/junit5/expected-exception-example/