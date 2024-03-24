## ✏️자바에서 숫자와 연산

> 자바에서 정확한 숫자 연산을 위해 신경써야 할 사항들..
> 특히 ***돈 계산*** 할떄! 😋

<br/>

### 참고: 실수의 종류

|  이름  | 크기(byte) | 용도      | 범위                        |
| :----: | :--------: | :-------- | :-------------------------- |
| float  |     4      | 작은 실수 | −3.4×10^38^ ~ +3.4×10^38^   |
| double |     8      | 일반 실수 | −1.7×10^308^ ~ +1.7×10^308^ |

<br/>

<br/>

## 1️⃣  부동 소수점(Floating Point) 과 고정 소수점(Fixed Point)

**부동 소수점 ( Floating Point )**   `실수를 근사하여 표현하는 방식`

➡️ 컴퓨터는 이진수(0과 1로 이루어진 숫자)를 사용하여 숫자를 저장하고 계산.
     이진수로는 정수만을 정확하게 표현, 실수는 ***근사적***으로 표현
➡️ 부동 소수점에서는 실수를 ***두 부분***으로 나누어 저장.
➡️ 같은 공간에서 더 넓은 범위를 저장할 수 있는 반면 정확도가 떨어진다

1. **가수 (Significand / Mantissa)**: 이진수로 표현된 실수의 유효 숫자 부분 
   이 부분은 소수점의 위치를 조절하여 숫자의 정밀도를 나타냄
2. **지수 (Exponent)**: 이진수로 표현된 실수의 자리수를 나타내는 부분 
   지수는 실제 숫자의 크기를 지수로 표현

<br/>

<img src="https://wikidocs.net/images/page/189025/float%EC%99%80_double.jpg" alt="종류에 따른 크기" style="zoom:30%;" />
출처: https://wikidocs.net/189025

<br/>

<br/>

```java
// 변수 선언
float a = 3.14f;
double b = 3.14d;
double b = 3.14;  //문자 붙이지 않은 경우 double 로 간주

float a = 3.14; //error - double은 float보다 커서 대입 불가!
```

<br/>

```java
// 문제 발생
double result = 0.1 + 0.2;
System.out.println("부동 소수점 결과: " + result); // 출력: 0.30000000000000004
```

</br>

<div align="center">

***0.00000000000000004 는 대체 어디서..? 🤔***

</div>

컴퓨터는 이진수로 숫자를 표현하고 부동 소수점을 사용하여 실수를 나타낸다.
하지만 0.1과 0.2는 이진수로 정확하게 표현할 수 없는 무한소수!!

</br>

0.1을 표현하면 0.0001100110011001100110011001100110011001100110011..
0.2를 표현하면 0.001100110011001100110011001100110011001100110011..

</br>

➡️ 이진수 표현의 한계로 인해 0.3과 완벽하게 일치하는 값이 아닌 근사치인 0.30000000000000004가 나오게 됨
➡️ 따라서 컴퓨터는 이 둘을 더할 때 완벽한 정확성을 보장할 수 없음🥷

</br>

이러한 이유로 부동 소수점 연산에서는 오류가 발생할 수 있으며, 
정확한 숫자 연산이 필요한 경우에는 다른 방법을 사용하는 것이 권장.

</br>

</br>

**고정 소수점 ( Fixed Point )**   ` 소수부의 자릿수를 미리 정하여, 고정된 자릿수의 소수를 표현하는 방식`

➡️ 제한된 자릿수로 인해 표현할 수 있는 범위가 매우 작음
➡️ **BigDecimal** 클래스를 사용
➡️ 정수부는 일반적인 이진수 표기법을 따릅니다.
➡️ 부호 : 0이면 양수, 1이면 음수
➡️ 소수부 남은 부분은 0으로 패딩

</br>

<img src="https://blog.kakaocdn.net/dn/d5M4tb/btrb1wUvUcB/XCrOt5QYGeTXtoOimqXG5k/img.png" alt="img" style="zoom:50%;" />
출처: https://nkt-docs.tistory.com/46

</br>

![img](https://gguguk.github.io/assets/img/post_img/floating_point_example.png)
출처: https://gguguk.github.io/posts/fixed_point_and_floating_point/

</br>

</br>

```java
// 변수 선언
BigDecimal num1 = new BigDecimal("0.1");
BigDecimal num2 = new BigDecimal("0.2");

BigDecimal result = num1.add(num2); // 고정 소수점 연산

System.out.println("고정 소수점 결과: " + result); // 출력: 0.3
```

</br>

</br>

**BigDecimal Class 🤔**  `정밀한 십진수 연산을 지원하기 위한 Java 클래스`

```java
import java.math.BigDecimal;

public class Main {
    public static void main(String[] args) {
        // 부정확한 생성자 사용
        BigDecimal number1 = new BigDecimal(0.1);
        System.out.println("부정확한 생성자 사용: " + number1); // 부정확한 결과 출력
        
        // 올바른 valueOf 메소드 사용
        BigDecimal number2 = BigDecimal.valueOf(0.1);
        System.out.println("valueOf 메소드 사용: " + number2); // 정확한 결과 출력
    }
}
```

</br>

> **valueOf** 메서드는 double 값을 인수로 받아서 해당 값을 정확하게 BigDecimal로 변환
>
> value 메서드를 사용할 때에는 정확한 값을 넣어주기만 하면 되지만 생성자를 사용할 때에는 double을 인수로 받기 때문에 정확한 값을 전달하기가 어렵다. double 값은 정확한 이진 부동 소수점으로 표현될 수 없는 경우가 있기 때문에 생성자를 사용하여 BigDecimal을 생성할 때 부정확한 값이 생성될 수 있다.
>
> 예를 들어, 생성자를 사용하여 0.1을 BigDecimal로 만들 경우, 컴퓨터는 가장 근사치에 가까운 이진 부동 소수점 값을 선택하여 BigDecimal로 변환한다. 하지만 valueOf 메서드를 사용할 경우, 명시적으로 정확한 값인 0.1을 전달하여 BigDecimal을 생성하므로 부정확한 값이 발생하지 않는다.



</br>

</br>

</br>

참고: https://junhyunny.github.io/java/calculate-number-in-java/
         https://wikidocs.net/189025
         https://www.tcpschool.com/java/java_datatype_floatingPointNumber