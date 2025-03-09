# Garbage Collection

<br/><br/>

## 1. Java 메모리 구조

### 1-1. JVM 메모리 구조

<img src="https://blog.kakaocdn.net/dn/pjywN/btqSduBXLIK/2QEL5c2nEJXRm0cyhvwxF1/img.png" alt="Untitled" style="zoom:50%;" />



<br/>

### 1-2. Heap 영역, Stack 영역, Method 영역 등의 역할 및 특징

- `Heap` 영역

  - **동적 데이터가 저장**되는 영역
  - 프로그램 실행 중에 생성되는 인스턴스나 객체들이 저장되는 공간
  - Heap 영역은 메모리가 허용하는 한 크기가 자동으로 늘어나거나 줄어들며, **가비지 컬렉터**에 의해 더 이상 참조되지 않는 객체들이 정리

- `Stack` 영역
  - **정적 데이터가 저장**되는 영역

  - 주로 지역 변수, 매개 변수, 리턴 값 등이 저장

  - 함수 호출이 발생할 때마다 해당 함수의 스택 프레임이 생성되어 스택 영역에 쌓이며, 함수가 종료되면 해당 함수의 스택 프레임은 제거

- `Method` 영역
  - 클래스 정보, 전역 변수, 상수, 코드 등이 저장되는 영역
  - **JVM에 의해 구성**되며, 프로그램 시작부터 종료 시까지 유지되는 영역




<br/><br/>

## 2. Java 메모리 관리

### 2-1. 객체 생성과 메모리 할당 과정

- Java에서 객체를 생성하려면 `new` 키워드를 사용

  ```java
  Student student = new Student();
  ```

- `Student` 라는 새로운 객체를 생성하고, 이 객체에 대한 참조를 `student`라는 변수에 저장

- `new` 키워드가 사용되면 JVM은 Heap 영역에서 해당 객체를 저장하기 위한 충분한 메모리 공간 탐색

<br/>

### 2-2. 객체 참조 및 접근 방식

- 생성된 객체는 참조 변수를 통해 접근

- 참조 변수는 `Stack` 영역에 저장되며, 실제 객체를 가리키는 **포인터 역할**

- 객체의 메소드를 호출하거나, 속성에 접근하기 위해서는 이 참조 변수를 통해 이루어짐

  ```java
  student.getName();
  ```

  -  `student`라는 참조 변수를 통해 `getName`이라는 메소드를 호출하여 객체의 이름을 반환



<br/><br/>

## 3. Java Garbage Collection이란?

### 3-1. 가비지 컬렉션의 필요성 및 역할

- Java 프로그램이 실행되는 동안 **계속해서 새로운 객체**가 생성
- 일부 객체는 더 이상 필요하지 않게 되는데, 이런 불필요한 객체들이 **메모리에 계속 남아** 있음
- 메모리 공간이 점차 줄어들어 결국에는 **프로그램의 성능 저하나 메모리 부족** 등의 문제
- *💡가비지 컬렉션은 이런 문제를 방지하기 위해 필요하다.*

<br/>

> **가비지 컬렉션(Garbage Collection, GC)**은 Java의 메모리 관리 기법 중 하나로, JVM이 메모리의 **Heap영역**에 동적으로 할당된 메모리 중 사용되지 않는 부분을 **자동으로 회수**하는 기능

<br/>

- 가비지 컬렉션은 이런 더 이상 사용되지 않는 객체들을 자동으로 감지하여 메모리에서 제거
- 개발자가 직접 메모리를 관리하는 부담을 덜어줌
  - 개발자는 필요한 객체를 생성하고 사용하면 되고, 그 객체가 더 이상 필요 없게 되면 가비지 컬렉터가 알아서 메모리에서 제거
- 단, 개발자가 메모리가 언**제 해제되는지 정확하게 알 수 없다**는 단점이 있다.



<br/><br/>

### 3-2. 가비지 컬렉션의 기본 원리 설명 : 도달 가능성과 Mark and Sweep

<img src="https://abiasforaction.net/wp-content/uploads/2021/05/xMark_Sweep_Compact.png.pagespeed.ic.3XG4GWQHMt.webp" alt="Mark and Sweep 과정" style="zoom:70%;" />

- 가비지 컬렉션의 기본 원리는 **`도달 가능성(Reachability)`**
- JVM은 **`Root Set`**이라는 기준점에서 시작해서 참조를 따라가며 도달할 수 있는 객체들을 '**도달 가능한 객체**'로 판단
  - `Root Set`은 Java 스택의 지역 변수나 입력 매개변수, 네이티브 스택의 JNI 참조, 메소드 영역의 정적 변수 등이 포함
- JVM은 `Root Set`에서 시작하여 참조를 따라가며 도달할 수 있는 모든 객체를 **마크**한다. 
- 마크되지 않은 객체, 즉 Root Set에서 참조를 따라 도달할 수 없는 객체들은 '**도달 불가능한 객체**'로 간주되며, 이런 객체들은 쑤레기로 취급
  - 이 과정을 **`Mark 단계`**
-  **도달 불가능한 객체들 (= Grabage) 은 가비지 컬렉터에 의해 **메모리에서 제거** 
- 가비지 컬렉터는 이런 가비지들을 찾아내어 그 메모리를 회수하고**, 필요에 따라 회수된 메모리를 재사용 가능한 상태**로 만들어줌
  - 이 과정을 **`Sweep 단계`**

<br/><br/>

## 4. Heap 영역의 메모리 구조와 Garbage Collection

### 4-1. Heap 영역의 메모리 구조

<img src="https://lh4.googleusercontent.com/RlpxXx62qN0d3x6uc2qlfOYv9SfS9DX-XZYSCJn_pXIbyuSGTxdSjx8mc4nH7H7A57EuE6qnqyryLqpDUANhlsL0nNnWc6HuHtQp1c4k3meXE1kJLppHAu5Br3_CIdoOw4SQSqrI" alt="Java 8부터 Permanent 영역은 Native Method Stack에 편입되었다." style="zoom:60%;" />

> Java 8부터 Permanent 영역은 Native Method Stack에 편입되었다.

- JVM의 힙 영역은 동적으로 **레퍼런스 데이터가 저장되는 공간**으로서, 가비지 컬렉션에 대상이 되는 공간
- Heap 영역은 처음 설계될 때 다음의 2가지를 전제 (**Weak Generational Hypothesis**)로 설계
  1. 대부분의 객체는 금방 접근 불가능한 상태(Unreachable)가 된다.
  2. 오래된 객체에서 새로운 객체로의 참조는 아주 적게 존재한다.
- 즉, 객체는 대부분 일회성이며, 메모리에 오랫동안 남아있는 경우는 드물다
- 효율적인 메모리 관리를 위해 이러한 특성을 이용해서 객체의 생존 기간에 따라 **물리적으로 Heap 영역을 나누게** 되었고, `Young` 과 `Old` 2가지 영역으로 설계

<br/>

### Young Generation

- 새롭게 생성된 객체가 할당(Allocation)되는 영역
- 대부분의 객체가 금방 Unreachable 상태가 되기 때문에, 많은 객체가 Young 영역에 생성되었다가 사라짐
- Young 영역에 대한 가비지 컬렉션 = `Minor GC`
- Young 영역은 다시 Eden, survivor 0, survivor 1으로 나뉨
  - Eden : new를 통해 새로 생성된 객체가 위치, 이곳에서 GC 후 살아남은 객체는 survivor로 이동
  - survivor 0 / survivor 1 : 최소 1번 이상의 GC에서 살아남은 객체가 위치
    -  0와 1 둘 중 하나는 반드시 비어 있어야 함

<br/>

### Old Generation

- Young영역에서 Reachable 상태를 유지하여 살아남은 객체가 복사되는 영역
- Young 영역보다 크게 할당되며, 영역의 크기가 큰 만큼 가비지는 적게 발생
- Old 영역에 대한 가비지 컬렉션을 `Major GC` 또는 `Full GC`라고 부름



<br/>

### 4-2. Minor GC와 Major GC

<img src="https://user-images.githubusercontent.com/61372486/128226448-582cb281-4401-4c1d-964c-5d806a767f0f.png" alt="ㅇ" style="zoom:37%;" />

### Minor GC

Minor GC는 **Eden 영역이 꽉차게 된 경우 발생**하며, Young 영역의 크기가 작기 때문에 **속도가 빠름**
보통은 0.5초에서 1초 사이!

1. 처음 생성된 객체는 Young 영역의 Eden에 위치
2. Eden 영역이 꽉차게 되면 `Minor GC`가 실행
3. Eden영역에서 살아남은 객체와 survivor 영역에서 살아남은 객체들은 비어있는 survivor 영역으로 이동
4. 이용하지않는 객체들은 메모리가 해제되고, 살아남은 객체는 age가 1씩 증가
5. 위의 과정을 반복

<br/>

### Major GC

Major GC는 **Old 영역이 꽉차게 된 경우 발생**하며, Old영역의 크기가 크기 때문에 속도가 Minor GC에 비해 **상대적으로 느림**
보통 10배 이상의 시간ㅜㅜ

1. 객체의 age가 일정한 값에 도달하게 되면 Old 영역으로 이동
2. Old 영역이 꽉차게 되면 `Major GC`가 실행
3. 위의 과정을 반복

<br/>

### 4-3. Stop-The-World

![ㄴ](https://abiasforaction.net/wp-content/uploads/2021/05/xStop_The_World_Pauses.png.pagespeed.ic.tyKN1R9wFh.webp)

- 가비지 컬렉션은 객체에 할당된 메모리를 해제하기 전에 애플리케이션 동작을 멈추도록!!

- 여기서 애플리케이션 동작이 멈춘다는 것은 GC와 관련된 스레드를 제외한 모든 스레드가 멈춘다는 의미
  <br/>

  1. **메모리 단편화 관리**

     할당된 메모리를 해제하는 과정에서 메모리 공간이 남게되고, 메모리 단편화가 발생하게 된다. 보통은 이를 해결하기 위해 **Compaction** 작업을 하게되는데, 이때 **객체를 새로운 주소로 이동**시키고 **다시 주소를 참조**하는 과정을 진행하므로 stop-the-world가 필수로 선행되어야한다.
     <br/>

  2. **객체 일관성**

     Garbage Collector가 더 이상 사용되지 않는 객체를 탐지하고 마킹하는 작업을 수행하는데, 이 과정에서 메모리 내의 객체들의 상태가 변경될수도 있고, 다른 스레드가 객체를 참조할 수도 있다. 이 과정에서 예기치 못한 오류가 생길 확률이 크다.

     예를 들어 Garbage Collector가 마킹한 객체를 스레드가 동시에 참조했다고 가정하면, 나중에 다시 호출 됐을 때 이미 객체는 메모리 해제되어 존재하지 않기 때문에 예기친 못한 오류를 만날 수 있다.

<br/>

- 단, 너무 자주 발생하거나 긴 시간 동안 지속될 경우 애플리케이션의 성능이 떨어질수있기 때문에 적절한 가비지 컬렉터를 사용하고, 가비지 컬렉션에 대한 최적화 작업(GC 튜닝)을 해야 함><

<br/><br/>

## 5. Garbage Collector 종류

Java에서는 다양한 가비지 컬렉터를 제공하고 있다. 각 가비지 컬렉터는 특정한 알고리즘과 전략을 사용하여 메모리를 관리하기 때문에, 각 특징을 알고 적절한 가비지 컬렉터를 사용하는 것이 중요하다.

### 5-1. Serial GC

싱글 스레드로 가비지 컬렉션을 수행하는 가장 간단한 형태의 가비지 컬렉터이다.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FVKJKl%2FbtqZoyLxsKB%2Fyelw9JtXxtRXUw8jABsjYK%2Fimg.png" alt="Untitled" style="zoom:33%;" />

- Young Generation과 Old Generation에서 `Mark-Sweep-Compact` 알고리즘을 사용

- 가비지 컬렉션 동작 동안 JVM의 다른 작업을 모두 중단

- 하지만 보통 실무에서 사용하는 경우는 없다. 디바이스 성능이 안좋아서 CPU 코어가 1개인 경우에만 사용한다.

- `-XX:+UseSerialGC` 옵션으로 활성화

  ```bash
  java **-XX:+UseSerialGC** -jar Application.java
  ```

<br/>

### 5-2. Parallel GC

**Java 8 이하**의 버전에서 기본으로 설정되어있는 가비지 컬렉터이다.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FLt8SI%2FbtqZpUghb6U%2FbWL987lUHZTGe51qHfoOVk%2Fimg.png" alt="Untitled" style="zoom:50%;" />

- Parallel GC는 멀티스레드를 활용하여 가비지 컬렉션을 병렬로 처리하는 가비지 컬렉터

- Young Generation에서 `Mark-Copy`를, Old Generation에서 `Mark-Sweep-Compact`를 사용
   → Mark Sweep Compation 알고리즘

- 가비지 컬렉션 동안 JVM의 다른 작업을 모두 중단하지만, 병렬 처리로 인해 전체 가비지 컬렉션 시간을 단축

- `-XX:+UseParallelGC` 옵션으로 활성화

  ```bash
  java **-XX:+UseParallelGC** -jar Application.java
  ```

- **Parallel Old GC**

  - Parallel GC는 Yound 영역에 대해서만 병렬 처리 방식을 사용했지만, Parallel Old GC는 Old영역까지 병렬 처리 방식을 사용

  - Mark Sweep Compation 알고리즘 대신 개선된 Mark Summary Compation 알고리즘을 사용.

  - `-XX:+UseParallelGCThreads=n` 옵션으로 멀티 스레드 개수를 지정

    ```bash
    java **-XX:+UseParallelGC** **-XX:ParallelGCThreads=4** -jar Application.jar
    ```

<br/>

### 5-3. CMS GC : Concurrent Mark Sweep GC

CMS GC는 최대한 'Stop-The-World' 일시 중단을 줄이기 위해 만들어진 가비지 컬렉터

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FchM1aO%2FbtqZtAafO9I%2Fx5ieeSoLcjfbMftBS6pkLK%2Fimg.png" alt="Untitled" style="zoom:30%;" />

- GC 대상을 파악하는 과정이 복잡한 여러 단계로 수행되기 때문에 다른 GC 대비 CPU 사용량이 높음

- 애플리케이션 중단 시간을 최소화 할 수 있지만 메모리 단편화가 발생 할 수 있음

- Old Generation에서 `Concurrent Marking`과 `Sweeping`을 사용

- CMS GC는 Java 9 이후부터 deprecated되었고, 결국 **Java14에서는 사용이 중지**

- **`-XX:+UseConcMarkSweepGC`** 옵션으로 활성화

  ```bash
  java **-XX:+UseConcMarkSweepGC** -jar Application.java
  ```



<br/>

### 5-4. G1 GC : Garbase-First GC

**Java 9 이상**의 버전에서 기본으로 설정되어있는 가비지 컬렉터

- 4GB 이상의 힙 메모리, stop-the-world 시간이 0.5초 정도 필요한 상황에서 사용하며, Heap 크기가 클수록 잘 동작
  → Heap이 너무 작을 경우는 미사용 권장ㅜㅜ

- 기존의 GC 알고리즘은 Heap 영역을 물리적으로 고정된 Young/Old 영역으로 나눠서 사용했지만, G1 GC는 새로운 논리적 단위인 **Region**이라는 개념을 사용

  - 전체 Heap 영역을 **Region**이라는 영역으로 분할하여 상황에 따라 Eden, Survivor, Old등의 역할을 동적으로 부여

    <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbfoIkH%2FbtqZyv7jRen%2FKvssCKeoo9rq56Uh3N1P60%2Fimg.png" alt="전체 영역이 Heap, 하나하나가 Region" style="zoom:40%;" />

  - 전체 영역이 Heap, 하나하나가 Region

  - Humonogous: Region 크기의 50%를 초과하는 큰 객체를 저장하기 위한 공간

  - Available/Unused: 아직 사용되지 않은 Region

  <br/>

- **Garbage-First** : 다른 알고리즘처럼 전체 Heap 영역을 한 번에 처리하는 것이 아니라, 나누어진 영역 중 가비지가 많은 영역부터 처리하기 때문에 GC 빈도가 줄어들고 효율적

- 전체 힙을 여러 개의 작은 영역으로 분할하여 관리하므로, 메모리 단편화를 최소화하고 효율적으로 메모리를 관리

- 공간 부족 상태를 조심 → Minor GC, Major GC를 수행하고 나서도 여유공간이 부족하게 되면 Full GC(Heap 영역 전체 GC)가 발생하는데, 이 GC는 싱글 스레드로 동작

- **`-XX:+UseG1GC`** 옵션으로 활성화

  ```bash
  java **-XX:+UseG1GC** -jar Application.java
  ```



<br/>

### 5-5. Shenandoah GC

CMS GC가 가진 메모리 단편화, G1이 가진 pause의 이슈를 해결한 가비지 컬렉터

![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FqDU6s%2FbtrhdlORpiI%2Fu1dWpv58U0Ub09S7NWbIFK%2Fimg.png)

- RedHat에서 개발하고, JDK 12 버전에서 릴리즈

- CMS의 메모리 단편화, G1의 stop-the-world 이슈를 개선

- 일명 low-pause GC 라고 불리며, 큰 가비지 컬렉션을 적은 횟수로 수행하는 것이 아닌 작은 가비지 컬렉션을 여러 번 수행

- 작은 단위의 가비지 컬렉션을 자주 수행하기 위해 동시성(Concurrency)을 보장

  - 즉, CPU를 더 사용하는 대신 stop-the-world(pause) 시간을 줄임

- Heap 사이즈에 영향을 받지않고 **일정한 pause 시간**이 소요

- **`-XX:+UseShenandoahGC`** 옵션으로 활성화

  ```bash
  java **-XX:+UseShenandoahGC** -jar Application.java
  ```





<br/><br/><br/>

참고:

https://steady-coding.tistory.com/305

https://abiasforaction.net/understanding-jvm-garbage-collection-part-2/

https://www.javamadesoeasy.com/2016/10/jvm-heap-memory-hotspot-heap-structure.html

https://www.javacodegeeks.com/2015/03/minor-gc-vs-major-gc-vs-full-gc.html

https://velog.io/@cham/JAVA-GCGarbage-Collector

https://abiasforaction.net/understanding-jvm-garbage-collection-part-2/

https://memostack.tistory.com/229

https://kchanguk.tistory.com/173