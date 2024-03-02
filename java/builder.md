## 빌더 (Builder)

<br/>

### 🤔WHAT?

<img src="https://raw.githubusercontent.com/silverpoodle/TIL/main/images/image-20240302212340592.png" alt="image-20240302212340592" style="zoom:67%;" />

출처: https://inpa.tistory.com/entry/GOF-%F0%9F%92%A0-%EB%B9%8C%EB%8D%94Builder-%ED%8C%A8%ED%84%B4-%EB%81%9D%ED%8C%90%EC%99%95-%EC%A0%95%EB%A6%AC

<br/>

<br/>

### 🤔WHEN?

1. 생성자의 인자가 많은 경우

2. 생성자의 인자들 중에 필수적 인자와 선택적 인자가 혼합되어 있는 경우

3. **Immutable 객체를 생성하고 싶은 경우**

   > 불변객체?
   >
   > 



<br/>

<br/>

### 🤔**빌더 패턴의 장점**

1. **매개변수의 순서와 개수에 무관한 생성:** 빌더 패턴은 매개변수의 순서나 개수에 관계없이 객체를 생성할 수 있어 가독성이 향상되고 명확한 코드 작성이 가능

2. **필수 및 선택적 매개변수 설정 가능:** 필수 매개변수와 선택적 매개변수를 효과적으로 다룰 수 있어 객체 생성 시 유연성을 제공
   -> 필수 매개변수는 빌더의 생성자로, 선택적 매개변수는 해당 매개변수를 설정하는 메소드로 설정 가능

3. **불변성 보장:** 빌더 패턴을 사용하면 생성된 객체는 불변성을 가질 수 있어 스레드 안전성과 예측 가능한 상태를 제공

<br/>

### 🤔**빌더 패턴의 단점**

1. **코드의 복잡성 증가:** 빌더 클래스를 정의하고 사용하는 것이 추가 코드 작성이 필요하므로 간단한 객체의 경우에는 코드가 더 복잡
2. **메모리 사용 증가:** 객체 생성 시에 빌더를 통해 생성하는 경우, 중간 단계의 객체들이 불필요하게 메모리에 생성될 수 있어 성능에 영향



<br/>

<br/>

<br/>

## Simple Builder Pattern

*by Effective Java*

**빌더(Builder) 클래스가 구현할 클래스의 정적 내부 클래스(Static Inner Class)Visit Website로 구현**

`static innter Builder Class + private Constructor`

<img src="https://raw.githubusercontent.com/silverpoodle/TIL/main/images/image-20240302215107909.png" alt="image-20240302215107909" style="zoom:70%;" />

1. **하나의 빌더 클래스, 하나의 대상 객체**

   Simple Builder Pattern에서는 하나의 빌더 클래스가 하나의 대상 객체 생성만을 담당합니다. 이로써 클래스 간의 관계를 명확하게 파악할 수 있으며, 코드의 유지보수성을 높일 수 있습니다.

2. **대상 객체 초기화는 빌더 객체에 의존**

   대상 객체는 오로지 빌더 객체에 의해 초기화됩니다. 생성자를 외부에 노출시키지 않기 위해 생성자를 private로 선언하고, 내부 빌더 클래스에서 private 생성자를 호출하여 빌더 객체에 의해 초기화되도록 설계합니다.

3. **인스턴스화의 독립성**

   Static으로 선언된 내부 클래스는 외부 클래스의 인스턴스 없이도 생성될 수 있습니다. 이는 빌더 클래스의 인스턴스가 생성될 때마다 새로운 빌더 객체를 생성할 수 있게 하므로, 독립적인 빌더 객체를 사용하여 다양한 객체를 생성할 수 있습니다.

4. **순환 종속성 방지** 

   만약 내부 클래스를 일반 내부 클래스로 선언한다면, 빌더 객체를 생성할 때 외부 클래스의 인스턴스를 먼저 생성해야 합니다. 이로 인해 빌더가 최종적으로 생성할 클래스의 인스턴스를 먼저 생성해야 하는 모순이 발생할 수 있습니다. Static 내부 클래스는 이러한 문제를 해결하여 빌더 패턴의 목적을 명확히 합니다.

<br/>

<br/>



## Lombok @Builder?

@Builder 어노테이션만 붙여주면 클래스를 컴파일 할 때 자동으로 클래스 내부에 빌더 API 생성!
이때 만들어지는 빌더는 **심플 빌더 패턴**.

<br/>

🤔**클래스에? 생성자에?**

```
클래스에 붙이면 모든 필드가 선택적으로 취급되므로, 기본적으로는 모든 필드에 대한 빌더 메서드가 생성. 이는 불필요한 메서드들이 생성될 수 있음을 의미하기 때문에 지양하도록!

생성자에 @Builder 어노테이션을 사용하면, 해당 생성자만을 위한 빌더 메서드가 생성
-> 필요한 필드만을 선택하여 객체를 생성할 수 있따
```

<br/>

🤔**근왜직만? 근데 왜 직접 만들어?**ㅋ

```
원하는 대로 빌더를 커스터마이징~
-> 해당 코드의 의도와 동작을 명확히 이해할 수 있따

굳이...?
```

<br/>

<br/>

## Director Builder Pattern

*by GoF*

**빌더를 받아 조립 방법을 정의한 클래스 "Director"**
 **-> 잡한 객체의 생성 알고리즘과 조립 방법을 분리하여 빌드** 

![Builder pattern - Wikipedia](https://upload.wikimedia.org/wikipedia/commons/thumb/f/f3/Builder_UML_class_diagram.svg/500px-Builder_UML_class_diagram.svg.png)

**디렉터 빌더 패턴은 여러가지의 빌드 형식을 유연하게 처리하는 것에 목적!**



<br/>

<br/>

## 정적 팩토리 메소드?

**정적 팩토리 메소드:**

1. **이름 부여**: 정적 팩토리 메소드는 이름을 가집니다. 이로 인해 코드의 가독성이 향상되고, 자주 사용되는 메소드를 구분하기 쉬워집니다.

2. **객체 재사용**: 호출할 때마다 새로운 객체를 생성할 필요가 없습니다. 이미 생성된 객체를 재사용할 수 있어 성능을 향상시킬 수 있습니다.

3. **하위 자료형 반환**: 반환값의 자료형을 유연하게 결정할 수 있습니다. 이는 인터페이스 기반 프레임워크에서 유용하게 활용될 수 있습니다.

4. **형인자 자료형 편의성**: 형인자 자료형 객체를 생성할 때 편리합니다. 컴파일러가 형인자를 스스로 추론할 수 있도록 도와줍니다.

**빌더 패턴:**

1. **선택적 인자 다루기**: 선택적으로 전달되는 인자들을 효과적으로 다룰 수 있습니다. 이는 생성자나 정적 팩토리 메소드로는 해결하기 어려운 여러 선택적 인자를 가진 객체를 생성하는 데 유용합니다.

2. **클라이언트 코드 가독성**: 클라이언트는 필수 인자를 생성자로 전달하고, 나머지 선택적 인자를 빌더의 메소드를 통해 설정하여 가독성이 좋은 코드를 작성할 수 있습니다.

3. **불변성 보장**: 빌더 패턴을 사용하면 객체를 불변하게 만들기 쉽습니다. 설정 메소드를 통해 값을 변경하는 것이 아닌, 새로운 불변 객체를 생성하기 때문입니다.

**선택적 인자가 많은 경우에는 빌더 패턴을, 이름을 통한 가독성과 객체 재사용은 적팩메~!** 

<br/>

```java
// Static Factory Method

public class MemberFactory {
    public static class Member {
        private UUID memberId;
        private String username;
        private String email;

        private Member(UUID memberId, String username, String email) {
            this.memberId = memberId;
            this.username = username;
            this.email = email;
        }
        
        public static Member createMember(String username, String email) {
            UUID memberId = UUID.randomUUID();
            return new Member(memberId, username, email);
        }
    }

}

```

<br/>

```java
//Builder
public class MemberBuilder {
    private UUID memberId;
    private String username;
    private String email;

    public static class Builder {
        private UUID memberId;
        private String username;
        private String email;

        public MemberBuilder builder() {
            this.memberId = UUID.randomUUID();
            return new MemberBuilder(this);
        }
    }

    private MemberBuilder(Builder builder) {
        this.memberId = builder.memberId;
        this.username = builder.username;
        this.email = builder.email;
    }

}
```

