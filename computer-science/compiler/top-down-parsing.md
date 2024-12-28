# Top-Down Parsing

Top-Down Parsing은 입력 문자열을 가장 상위 기호에서 시작해 점진적으로 구체적인 하위 구조로 분해하면서 문법을 분석하는 방법
입력 문자열이 주어진 문법에 따라 생성될 수 있는지 확인하는 데 사용

<br/><br/>



### LL Parsing

LL Parsing은 입력을 왼쪽에서 오른쪽으로 읽으면서, 왼쪽에서 오른쪽으로 파싱 트리를 구성하는 방법입니다. 
LL은 Left-to-right scanning과 Leftmost derivation을 의미합니다. 여기서 LL Parsing은 두 가지 유형으로 나눌 수 있습니다:

- **LL(1) Parsing**: 하나의 토큰을 미리 보고 파싱을 결정하는 방법.
- **LL(k) Parsing**: k개의 토큰을 미리 보고 파싱을 결정하는 방법.



<br/>
<br/>

### Grammar without Backtracking

백트래킹 없는 문법은 구문 분석 중 다시 돌아가서 다른 경로를 시도하지 않아도 되는 문법입니다. 
LL(1) 문법은 일반적으로 백트래킹이 없는 문법입니다.

<img src="https://github.com/silverpoodle/typora-images/blob/main/image-20240612181756908.png?raw=true" alt="image-20240612181756908" style="zoom:67%;" />

<br/>
<br/>

### LL(k) Grammar

LL(k) 문법은 k개의 토큰을 미리 보고 파싱을 결정할 수 있는 문법을 의미합니다. 

1. LL(1) Grammar

   LL(1) 문법은 한 개의 토큰을 미리 보고 파싱을 결정하는 문법입니다. 
   LL(1) 파서는 입력을 왼쪽에서 오른쪽으로 읽으며, 좌측에서부터 가장 먼저 유도되는 파생을 따라 파싱 트리를 구축합니다. 
   LL(1) 문법에서는 각 논터미널과 그 문법 규칙이 단 하나의 토큰에 의해 결정됩니다.

   <br/>

   <img src="https://github.com/silverpoodle/typora-images/blob/main/image-20240612182236085.png?raw=true" alt="image-20240612182236085" style="zoom:67%;" />

   

   2. LL(2) Grammar

      LL(2) 문법은 두 개의 토큰을 미리 보고 파싱을 결정하는 문법입니다.
      LL(2) 파서는 입력을 왼쪽에서 오른쪽으로 읽으며, 좌측에서부터 가장 먼저 유도되는 파생을 따라 파싱 트리를 구축합니다. 
      LL(2) 문법에서는 각 논터미널과 그 문법 규칙이 두 개의 토큰에 의해 결정됩니다.

      <br/>

      <img src="https://github.com/silverpoodle/typora-images/blob/main/image-20240612182455202.png?raw=true" alt="image-20240612182455202" style="zoom:67%;" />

3. LL(K)

   현재 위치에서 생성해야 할 터미널 k개를 보고서 적용할 생성규칙을 결정적으로 선택할 수 있는 문법입니다.

   <br/>

   ```
   For A → α | β
    FIRSTk(α) ∩ FIRSTk(β) = ф
   ```

   

<br/>
<br/>

### First & Follow

First와 Follow 집합은 파싱 과정에서 중요한 역할을 합니다.

- **First(A)**: 문자열 A로 시작할 수 있는 모든 터미널 기호들의 집합.
- **Follow(A)**: 문자열 A 다음에 나올 수 있는 모든 터미널 기호들의 집합.

```
 S → AbB | BbB
 A → aBb | bBb | cBb
 B → d | e | f
 FIRST(A) = FIRST(aBb) ∪ FIRST(bBb) ∪ FIRST(cBb) = { a, b, c }
 FIRST(B) = FIRST(d) ∪ FIRST(e) ∪ FIRST(f) = { d, e, f }
 FIRST(S) = FIRST(AbB) ∪ FIRST(BbB) = { a, b, c, d, e, f }
```



<br/>
<br/>

### 고려할 것들

#### Left Recursion

좌측 재귀는 Top-Down Parsing에서 문제가 될 수 있습니다. 좌측 재귀를 제거해야 LL 파서를 구축할 수 있습니다. 예를 들어, 다음과 같은 좌측 재귀 문법이 있다고 가정합니다:

```
A → Aα | β
```

이를 다음과 같이 변환합니다:

```
A → βA'
A' → αA' | ε
```

<br/>

#### Left Factoring

Left Factoring은 문법을 리팩토링하여 파싱 결정을 쉽게 하는 방법입니다. 동일한 접두사를 공유하는 규칙들을 분리합니다. 예를 들어:

```
A → αβ | αγ
```

이를 다음과 같이 변환합니다:

```
A → αA'
A' → β | γ
```



<br/>

#### LOOKAHEAD(A→α)

LOOKAHEAD는 파싱 결정 시 앞으로의 입력을 미리 보는 것입니다. 
A→α와 같이 특정 규칙을 결정하기 위해 다음 토큰을 확인합니다.

### Recursive-Descent Parser

재귀 하강 파서는 각 문법 규칙에 대해 하나의 재귀 함수를 사용하여 입력을 분석하는 파서입니다. 각 함수는 문법 규칙에 대응하며, 입력을 왼쪽에서 오른쪽으로 스캔하여 왼쪽에서 오른쪽으로 파싱 트리를 생성합니다.

### Predictive Parser

예측 파서는 미리 정의된 규칙과 LOOKAHEAD를 사용하여 입력을 예측하고 파싱합니다. LL(1) 파서가 대표적인 예입니다.

### 예시

이제 LL(1) 파서의 예시를 통해 이를 설명하겠습니다.

**문법:**

```
E → T E'
E' → + T E' | ε
T → F T'
T' → * F T' | ε
F → ( E ) | id
```

**First와 Follow 집합:**

- First(E) = First(T) = First(F) = { '(', 'id' }
- Follow(E) = { '$', ')' }
- Follow(E') = Follow(E)
- Follow(T) = { '+', '$', ')' }
- Follow(T') = Follow(T)
- Follow(F) = { '*', '+', '$', ')' }

**구문 분석 과정:**
입력 문자열: `id + id * id`

1. **E → T E'**
   - T → F T'
     - F → id
     - T' → ε
   - E' → + T E'
     - T → F T'
       - F → id
       - T' → * F T'
         - F → id
         - T' → ε
     - E' → ε

이 과정을 그림으로 나타내면 아래와 같습니다:

```plaintext
        E
       / \
      T   E'
     / \    \
    F  T'    + T E'
   /     \      / \
id       ε     T   E'
               / \
              F  T'
             /    \
           id     * F T'
                 / \
                F  T'
               /     \
             id       ε
```

이 예시를 통해 LL(1) 파서의 작동 방식을 시각적으로 이해할 수 있습니다.





>  Top-Down Parsing은 입력 문자열을 가장 상위 기호에서 시작해 점진적으로 구체적인 하위 구조로 분해하면서 문법을 분석하는 방법입니다. 
> LL Parsing은 가장 대표적인 Top-Down Parsing 기법으로, LL(1) 파서가 그 예입니다. 이를 위해 문법은 좌측 재귀를 제거하고, Left Factoring을 통해 파싱을 쉽게 만들며, First와 Follow 집합을 통해 파싱 결정을 내립니다. 
> Recursive-Descent 파서와 Predictive 파서는 이러한 원리를 기반으로 작동합니다.