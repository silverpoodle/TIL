# 형식 언어 (Formal Language)



## 1. 언어 (Language)

- language = set of `statements`
- statement = set of `alphabets`

<img src="https://github.com/silverpoodle/typora-images/blob/main/image-20240422202116582.png?raw=true" alt="image-20240422202116582" style="zoom:50%;" />

<br/>

**[정의 2.1] alphabet의 정의**

> alphabet T는 symbol들의 **유한집합**(finite set)이다.

<br/>

ex)

```tex
T1 = {ㄱ, ㄴ, ㄷ, ㄹ, ⋯, ㅎ, ㅏ, ㅑ, ㅓ, ㅕ, ⋯, ㅡ, ㅣ}
T2 = {A, B, C, D, ⋯, Z}
T3 = {main, int, char, long, ⋯ }
```

<br/>

**[정의 2.2] string 정의**

> Alphabet T에 대한 string은 sequence of one or more symbols (언어의 문장) 이다.

<br/>

ex)

```tex
T = {a, b}일 때
a, b, aa, ab, ba, bb, aaa, ⋯ 는 모두 T로부터 생성되는 string이다
```

<br/>

**[정의 2.3] string length**

> string의 길이는 string을 구성하고 있는 symbol들의 수 이고, 임의의 string ω의 길이는 | ω|로 표기한다

<br/>

ex)

```tex
ω = a1a2a3⋯ak이면 |ω| = k이
```

<br/>

**[정의 2.4] Concatenation**

> string을 연속으로 연결한 것이다.
>
> - 교환법칙 성립안함 ( u・v ≠ v・u)
> - u・v는 간단히 uv로 표기하며 u를 prefix, v를 suffix라 한다.
> - |uv| = |u| + |v|

<br/>

ex)

```tex
u = a1a2a3⋯an, v = b1b2⋯bm일 때
u・v = a1a2a3⋯anb1b2⋯bm
```

<br/>

**[정의 2.5]  Empty/Null string & Reverse String** 

> - 공백 스트링은 ε 또는 λ로 표기
> - ωR 은 string ω의 역순

<br/>

ex)

```json
ω = v1v2v3⋯vn이면, ωR = vn⋯v3v2v
uε = u = εu //어떤 문자열과 빈 문자열을 연결하면 원래의 문자열 
uεv = uv // 문자열 사이에 빈 문자열을 추가하면 단순히 u와 v를 연결한 것과 동일
```

<br/>

**[정의 2.6]  T*(universal set) 와 T+ (dagger) ** 

> - T * : **empty string을 포함**하여 T에 속하는 symbol로 이루어질 수 있는 모든 string들의 집합. 
> - **T +** : **empty string을 제외**하고 T에 속하는 symbol로 이루어질 수 있는 모든 string들의 집합. 
> - T + = T * - { ε }

<br/>

ex)

```json
T = {0}일 때, T* = { ε, 0, 00, 000, ⋯}, T+ = {0, 00, 000, ⋯}

T = {a, b}일 때, T* = { ε, a, b, aa, ab, ba, bb, aaa, aab, ⋯},
T+ = {a, b, aa, ab, ba, bb, aaa, aab, ⋯}

For u, v ∈ T*, uv ∈ T* // u와 v가 ∗T 에 속하는 문자열일 때, uv도 ∗T 에 속하는 문자열임
```



`※ alphabet T는 항상 유한집합, T *는 항상 무한집합 임의의 u, v ∈ T *에 대하여 uv ∈ T *이다. 
즉, T *는 alphabet T에 속하는 symbol로부터 생성할 수 있는 전체집합이다.`

<br/>

**[정의 2.7]  Language ** 

> **Language L is a subset of T***
>
> - 유한언어(finite language)와 무한언어(infinite language):
>   언어에 속하는 string의 수가 유한 개 or 무한 개 (ex 에서 L2만 유한 언어)

<br/>

ex)

```json
T = {a, b}일 때

L1 = T* = { ε, a, b, aa, ab, ba, bb, aaa, aab, ⋯},
L2 = { a, ba, aba }  //유한언어
L3 = { aᵖ | p는 소수 }
L4 = { aⁿbⁿ | n ≥ 1 }
```

`형식언어는 의미(semantics)를 논하지 않으며, 언어의 syntactic structure만 다르다. 즉, 형식언어 이론은 string 집합의 속성에 관한 이론이다.`

<br/>

**[정의 2.8]  Product of the languages** 

> **LL’ = { uv | u ∈ L and v ∈ L’ }** 
>
> - 두 언어 L과 L'의 곱(product)은 L・L'은 L에 속하는 string과 L'에 속하는 string을 접속한 것으로 간단히 LL'으로 나타낼 수 있다. (교환법칙 성립 안함)

<br/>

ex)

```json
L2{a, b} = { aa, ab, baa, bab, abaa, abab}
L3L4 = { aᵖ⁺ⁿbⁿ | p는 소수, n ≥ 1 }
```

<br/>

**[정의 2.11]  Transitive closure** 

> **L⁺ = L¹ ∪ L² ∪ L³ ∪  ...  Lⁿ = L* - L⁰**
>
> - 각 언어마다 고유의 알파벳 T가 존재하며 T로부터 만들 수 있는 string 전체의 집합이 T *이다. 
> - 언어는 T * 중에서 어떤 규칙에 적합한 string으로 정의된다.
> -  한 언어에 속하는 string을 그 언어의 문장(sentence)이라 한다.

<br/>

<br/>

<br/>

## 2. Grammar

- Language representation (언어 표현)
  - Finite language: list all strings 
  - Infinite language: finite representation 
- Finite representation (유한 표현)
  - Condition presentation: set representation =  집합 표현 방식으로 조건 제시법
  - Grammar: language generation system = 언어 생성 시스템인 문법
  - Recognizer = 언어 인식 시스템
- Grammar
  - VN: set of nonterminal symbol -> intermediate  symbol
  - VT : set of terminal symbol → alphabet
  - Grammar symbol = VN + VT = V (vocabulary)

<br/>

**[정의 2.12]  문법 구성 네 가지 항목 ** 

> **G = (VN, VT, P, S)** 
>
> - **VN** : nonterminal symbol의 유한 집합 → A, B, C 등 **대문자 사용** 
>   - 생성규칙에 의해 대체될 수 있는 기호들의 집합
> - **VT** : terminal symbol의 유한 집합 →  a, b, c 등 **소문자 사용** 
>   - 문법의 최종 출력물인 문자열의 구성 요소로 사용되는 기호들의 집합
> - **P** : 생성규칙(production rule)의 유한 집합 
> - **S** : VN에 속하는 symbol로 start symbol 혹은 sentence symbol → **대문자 S**
> - **V*** **string**  α,β,γ …
> - **VT*** **string**: ω
>
> - VN ∩ VT = ∅, VN ∪ VT =V

<br/>

ex)

```json
G = ({S,A}, {a,b}, P, S}
P : S → aAS,  S → a,  A → SbA,  A → ba,  A → SS

//첫 번째 규칙(S → aAS): 시작 심볼 S를 만나면, 그 다음에는 "a"와 "AS"가 올 수 있음
//두 번째 규칙(S → a): 시작 심볼 S를 만나면, 단순히 "a"를 생성
//세 번째 규칙(A → SbA): 비터미널 심볼 A를 만나면, 그 다음에는 "SbA"가 올 수 있음
//네 번째 규칙(A → ba): 비터미널 심볼 A를 만나면, 단순히 "ba"를 생성
//다섯 번째 규칙(A → SS): 비터미널 심볼 A를 만나면, 그 다음에는 두 개의 비터미널 심볼 S로 이루어진 문자열이 올 수 있음

// "S"로 시작하여 생성규칙을 따라가면 "a", "aa", "aab", "ab", "aba", "abab", "abaab", 등 다양한 문자열을 생성할 수 있게 된다.
```

<br/>

생성 규칙의 축약

```json
α → β1, α → β2 ⇔ α → β1 | β2
```

<br/>

**[정의 2.13]   Derivation (유도) ** 

> -  **‘⇒’**는 직접 유도(directly derive)된다는 의미
>   - α → β가 존재하고 γ,δ∈V *이면, γ α δ ⇒ γ β
> - **‘⇒ *’**는 0번 이상의 유도된 과정
>   - , α1, α2, α3,⋯ αn이 V *에 속하고 α1 ⇒ α2 ⇒ α3 ⇒ ⋯ ⇒ αn * 이 존재한다면 α1 ⇒*αn
> - **‘⇒+’**는 한 번 이상의 유도된 과정

<br/>

ex)

```json
G = ({S,A}, {a,b}, P, S}
P : S → aAS,  S → a,  A → SbA,  A → ba,  A → SS

//첫 번째 규칙(S → aAS): 시작 심볼 S를 만나면, 그 다음에는 "a"와 "AS"가 올 수 있음
//두 번째 규칙(S → a): 시작 심볼 S를 만나면, 단순히 "a"를 생성
//세 번째 규칙(A → SbA): 비터미널 심볼 A를 만나면, 그 다음에는 "SbA"가 올 수 있음
//네 번째 규칙(A → ba): 비터미널 심볼 A를 만나면, 단순히 "ba"를 생성
//다섯 번째 규칙(A → SS): 비터미널 심볼 A를 만나면, 그 다음에는 두 개의 비터미널 심볼 S로 이루어진 문자열이 올 수 있음

// "S"로 시작하여 생성규칙을 따라가면 "a", "aa", "aab", "ab", "aba", "abab", "abaab", 등 다양한 문자열을 생성할 수 있게 된다.
```

<br/>

`※ string α가 V *에 속한다( α∈V *) ≡ α는 nonterminal과 terminal로 구성된 string`

<br/>

**[정의 2.14]   Sentential form ** 

> **S ⇒ ω이고 ω가 V *에 속하면** ω를 **sentential form**이라 하고, 
> ω가 VT *에 속할 경우 ω를 **sentence**라고 한다. 
>
> 즉, *sentence는 nonterminal을 포함하지 않는 sentential form*이다

<br/>

ex)

```json
S  ⇒ aA ( 생성규칙 S → aA를 적용 )
	⇒ abS ( 생성규칙 A → bS를 적용 )
	⇒ abbB ( 생성규칙 S → bB를 적용 )
	⇒ abbaS ( 생성규칙 B → aS를 적용 )
	⇒ abba ( 생성규칙 S → ε를 적용 )

*S ⇒ abba

sentential form : aA, abS, abbB, abbaS, abba
sentence : abb
```

<br/>

`Sentence = string, teminal 만으로 구성 + 시작 기로호부터 유도 가능`

<br/>

**[정의 2.15]   Language L(G) ** 

> **L(G) = { ω | S ⇒ ω, ω∈VT * }**
>
> L(G)는 start symbol로부터 유도될 수 있는 모든 문장의 집합.

<br/>

ex1)

```json
//문법 G1에 대하여 L(G1)을 구하라.  
G1 = ({S}, {a}, P , S), P: S → a | aS }

// S에서 시작하여 생성규칙을 따라가면 다음과 같은 문자열을 생성할 수 있습니다:

// S → a
// S → aS → aa
// S → aS → aaS → aaa
// S → aS → aaS → aaaS → aaaa
// ...

// 이 과정을 보면, S를 대체하는 과정에서 매번 하나의 'a'가 추가됩니다. 
// 즉, S를 대체하는 과정에서 생성되는 문자열의 형태는 'a'가 1개 이상 연속해서 나타나는 형태

L(G1) = {aⁿ | n≥1}
```

<br/>

ex2)

```json
// 문법 G2에 대하여 L(G2)을 구하라.
G2 = ({O,E}, {a}, P , O), P: O → a | aE, E → aO
L(G2) = {a²ⁿ⁺¹ | n≥0 }
```

<br/>

ex3)

```json
// 문법 G3에 대하여 L(G3)을 구하라.
G3 = ({A,B,C}, {a,b,c}, P , A),
P: A → abc A → aBbc Bb → bB Bc → Cbcc
bC → Cb aC → aaB aC → aa

L(G3) = {aⁿbⁿcⁿ | n≥1 }
```

<br/>

ex4)

```json
// L1 = {aⁿbⁿ | n≥1}를 생성하는 문법을 고안해 보자.

//  'a'와 'b'의 개수가 같은 문자열로 구성
// 따라서 이 언어를 생성하기 위해서는 'a'와 'b'의 개수를 일치시키는 방법을 고려주어진 언어의 // 문자열은 'a'로 시작하여 'b'로 끝나야 하며, 중간에는 임의의 개수의 'a'가 올 수 있다.

// 1. 시작 심볼 S를 대체할 때, 첫째로 'a'를 생성하고, 그 뒤에 임의의 개수의 'a'를 생성한 후 'b'를 생성
// 2. 'aSb' 규칙을 반복적으로 적용하여 중간에 'a'가 반복되도록
// 3. 'a'만으로 문자열을 생성할 수 있도록 'a' 규칙도 포함됩니다.

S → aSb | a
```

<br/>

### Grammar and Language



<img src="https://github.com/silverpoodle/typora-images/blob/main/image-20240422230304167.png?raw=true" alt="image-20240422230304167" style="zoom:67%;" />

<br/>

<br/>

<br/>

## 문법의 분류

```
1. Type 0 문법 ( UG: unrestricted grammar )
	생성규칙에 제한을 두지 않는다.
	
2. Type 1 문법 ( CSG: context-sensitive grammar )
	모든 생성규칙 α → β에서 |α| ≤ | |이다.
	
3. Type 2 문법 ( CFG: context-free grammar )
	모든 생성규칙은 A → α의 형태를 갖는다.
	( A는 하나의 nonterminal이고, α는 V*에 속하는 string이다. )

4. Type 3 문법 ( RG: regular grammar )
	모든 생성규칙은 2가지 형태로 표현된다.
	(1) A → tB 혹은 A → t, 여기서 t∈VT*이고 A,B∈VN이다.
	(2) A → Bt 혹은 A → t, 여기서 t∈VT*이고 A,B∈VN이다
```

`※ (1)을 우선형 문법(right-linear grammar), (2)를 좌선형 문법(left-linear grammar)이라 한다`

<br/>

**[정의 2.16]  언어의 유형 ** 

> 1. regular language : 정규 문법(type 3)에 의해 생성되는 언어
> 2.   context-free language : CFG(type 2)에 의해 생성되는 언어 
> 3.  context-sensitive language : CSG(type 1)에 의해 생성되는 언어 
> 4. recursively enumerable set : UG(type 0)에 의해 생성되는 언어 

<br/>

`언어 포함 관계: RG ⊆ CFL ⊆ CSL ⊆ U`

<br/>

`※ 언어를 인식하는 인식 시스템 `
``1. 정규 언어 : 유한 오토마타 ( finite automata ) `
`2. 문맥 자유 언어 : pushdown automata `
`3. 문맥 의존 언어 : linear-bounded automata `
`4. unrestricted 언어 : Turing machine`

<br/>

ex)

```json
//언어 L(G2) = {aⁿbⁿ | n≥1 }를 생성하는 CFG를 구하시오

G2 = ({S,C}, {a,b}, P, S)
P: S → aCa, C → aCa | b
```

<br/>