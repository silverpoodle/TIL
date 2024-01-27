### java 실행 과정



#### 1. Compile - javac

#### 2. Class Loading - bytecode is loaded into memory, 

#### 3. ByteCode Excecution - JVM







<img src="https://media.geeksforgeeks.org/wp-content/uploads/java.jpg" alt="img" style="zoom: 60%;" />

<img src="https://media.geeksforgeeks.org/wp-content/uploads/jvm-3.jpg" alt="jvm" style="zoom: 25%;" />



# 자바의 특징

### OS에 독립적이다!!

### 메모리를 알아서 관리해준다!!

# 자바 컴파일 과정

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/440e0051-e1a6-4fc1-b7a8-96dc6ee9928e/6a1ec06b-5bdc-4c74-93f0-9e472fb4606b/Untitled.png)

<aside> 💡 **동적로딩?** → JVM에서 실행에 필요한 모든 클래스 파일을 메모리에 올려놓지 않고, 필요한 시점에 동적으로 메모리에 올리는 기술 가능한 적은 클래스 파일을 메모리에 올려 실행 할 수 있으므로 효율적이라고 할 수 있다.

</aside>

1. 개발자가 **자바 소스코드를 작성**합니다.
2. 자바 컴파일러가 자바 **소스파일을 컴파일** 합니다. 이때, 나오는 파일은 **자바 바이트 코드(.class)파일**로 아직 컴퓨터가 읽을 수 없고, 자바 가상 머신이 이해할 수 있는 코드임. 바이트코드의 각 명령어는 1바이트 크기의 Opcode와 추가 피연산자로 이루어져있음.
3. **컴파일된 바이트 코드**를 **JVM**의 **클래스 로더(Class Loader)**에게 전달
4. **클래스로더는 동적로딩**을 통해 필요한 클래스들을 로딩 및 링크하여 런타임 데이터 영역, **즉, JVM의 메모리에 올린다.**
5. 실행엔진은 **JVM 메모리에 올라온 바이트 코드들을 명령어 단위로 하나씩 가져와서 실행**한다. 해당 방식은 2가지로 나뉜다.

1. **인터프리터** : → 바이트 코드 명령어를 하나씩 읽고 해석하고 실행한다. **하나하나의 실행은 빠르나, 전체적인 실행 속도가 느리다**는 단점을 가진다.
2. **JIT 컴파일러** : → 인터프리터의 단점을 보완하기 위해 도입된 방식으로 바이트 코드 전체를 컴파일하여, 바이너리 코드로 변경하고 이후에는 해당 메서드를 더이상 인터프리팅 하지 않고, 바이너리 코드로 직접 살행하는 방식. **하나씩 인터프리팅하여 실행하는 것이 아니라 바이트 코드 전체가 컴파일된 바이너리 코드를 실행하는 것이기 때문에 전체적인 실행속도는 인터프리팅 방식보다 빠름**. `BUT` 컴파일 과정이라는 **비용이 발생함!!**

**⇒ 그래서 두개 같이 혼용에서 사용함.**

------

### 클래스로더의 동작

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/440e0051-e1a6-4fc1-b7a8-96dc6ee9928e/5564d22b-fe7d-4ea4-8bc0-9d327926af87/Untitled.png)

- 클래스 로더 세부 동작
  1. **로드** : 클래스 파일을 가져와 JVM의 메모리에 로드함.
  2. **검증** : 자바 언어 명세 및 JVM 명세에 명시된대로 구성되어 있는지 검사
  3. **준비** : 클래스가 필요로 하는 메모리 할당 (필드, 메서드, 인터페이스 등등)
  4. **분석** : 클래스의 상수 풀 내 모든 심볼릭 레퍼런스를 다이렉트 레퍼런스로 변경
  5. **초기화** : 클래스 변수들을 적절한 값으로 초기화 한다. (static 필드)

------

# JVM의 메모리 관리!

## 런타임 데이터 영역 (Runtime Data Area)

- 런타임 데이터 영역은 JVM의 메모리 영역으로 자바 어플리케이션을 실행할 때 사용되는 데이터들을 적재하는 영역

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/440e0051-e1a6-4fc1-b7a8-96dc6ee9928e/bbeccd21-4727-4b87-8852-9fa38241ec46/Untitled.png)

## 메서드(static) 영역

- 프로그램의 시작부터 종료가 될 때까지 메모리에 남게되는 영역.
- 정적 필드와 클래스 구조만을 가지고 있다.
  - 필드정보 : 멤버 변수의 이름, 데이터 타입, 접근 제어자의 정보
  - Method Info : 메소드 이름, return 타입, 함수 매개변수, 접근 제어자의 정보
  - Type Info : Class 인지 Interface 인지 여부 저장, Type의 속성, 이름 Super Class 의 이름

### Runtime Constant Pool

- 메서드 영역에 존재하는 별도의 관리영역
- 클래스 생성할때 참조해야 할 정보들을 상수로 가지고 있는 영역
- JVM은 이 Constant Pool을 통해 해당 메소드나 필드의 실제 메모리 상 주소를 찾아 참조!

## 스택 영역

- 지역변수, 파라미터, 리턴 값, 연산에 사용되는 임시 값 등이 생성되는 영역
- LIFO의 구조를 갖고, 변수에 새로운 데이터가 할당되면 이전데이터는 지워짐

```jsx
public class StackAreaEx {
	public static void main(String[] args) {
		int a = 5;	a = 4;	a = 3;	a = 2;
		System.out.println(a);
		for(int i=0; i<5; i++){
		}
//		System.out.println(i); 컴파일 에러
	}
}
```

## PC 레지스터

- 스레드가 생성될 때마다 생성되는 영역으로 프로그램 카운터, 즉 현재 스레드가 실행되는 부분의 주소와 명령을 저장하고 있는 영역

## 네이티브 메서드 스택 ( Native Method Stack)

- 자바 이외의 언어(C, C++, 어셈블리 등)로 작성된 네이티브 코드를 실행할 때 사용되는 메모리 영역으로 일반적인 C 스택을 사용한다.
- 보통 C/C++ 등의 코드를 수행하기 위한 스택을 말하며 (JNI) 자바 컴파일러에 의해 변환된 자바 바이트 코드를 읽고 해석하는 역할을 하는 것이 자바 인터프리터이다.

## 힙 영역

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/440e0051-e1a6-4fc1-b7a8-96dc6ee9928e/3486b27c-f10e-4b8b-bc1e-70533e1a8373/Untitled.png)

- new 키워드로 생성된 객체와 배열이 생성되는 영역
- 주기적으로 GC가 관하는 영역
- Heap 영역은 효율적인 GC를 위해 위와같이 크게 3가지 영역으로 나뉘어짐
- Young Generation 영역은 자바 객체가 생성되자마자 저장되고, 생긴지 얼마 안되는 객체가 저장되는 공간

### GC가 처리하는 과정

1. Heap 영역에 객체가 생성되면 최초로 Eden 영역에 할당이 됨.

2. 이영역에 데이터가 어느정도 쌓이게 되면 참조정도에 따라 Servivor의 빈 공간으로 이동되거나 회수됨

3. Young Generation 영역이 차게 되면 또 참조정도에 따라 Old영역으로 이동되거나 회수된다.

   이처럼 Young Generation과 Tenured Generation 에서의 GC를 **Minor GC**라고 한다.

4. **Old 영역**에 할당된 메모리가 허용치를 넘게 되면, Old 영역에 있는 모든 객체들을 검사하여 참조되지 않는 객체들이 한꺼번에 삭제되는 GC가 실행됨

   시간이 오래 걸리는 작업이고, 이 때 GC를 실행하는 쓰레드를 제외한 모든 스레드는 작업을 멈추게 된다.

   이 때를 ‘Stop-the-world’라고 한다. 이렇게 ‘Stop-the-world’ 가 발생하고 **Old 영역의 메모리**를 회수하는 GC를 **Major GC**라고 한다.
