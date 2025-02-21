# 유클리드 알고리즘 (Euclidean Algorithm)

<img src="https://www.inchcalculator.com/wp-content/uploads/2018/12/euclids-algorithm.png" alt="d" style="zoom:27%;" />

유클리드 알고리즘은 두 양의 정수의 `최대공약수(Greatest Common Divisor)`를 구하는 효율적인 방법

<br/>

<br/>

## 1. 원리

두 양의 정수 `a`, `b`에 대해서 a를 b로 나눈 나머지를 `r` 이라 하면(단, a > b)
**`a`와 `b`의 최대공약수**는 **`b`와 `r`의 최대공약수**와 같다.

```
GCD(a, b) = GCD(b, r)  (단, r은 a를 b로 나눈 나머지)
```

<br/><br/>

## 2. 구현 예시 (Java)

```java
// 재귀적 구현
public static int gcd(int a, int b) {
    if (b == 0) return a;
    return gcd(b, a % b);
}

// 반복문 구현
public static int gcd(int a, int b) {
    while (b != 0) {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return a;
}
```

<br/><br/>

## 3. 시간 복잡도

- O(log N) (N은 입력된 수 중 큰 수)
- 큰 수에 대해서도 !빠르게! 계산 가능



<br/><br/>



참고

https://www.inchcalculator.com/euclidean-algorithm-calculator/