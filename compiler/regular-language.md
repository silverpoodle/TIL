# 정규 언어(Regular Language)

## 1. Regular Grammar (정규 문법)

- Right linear grammar: : A → tB |  t
- Left linear grammar : A → Bt | a
  - A,B ∈ VN, t ∈ VT*
- Not regular grammar — A → aA | Bb | c 
  - `좌선형과 우선형이 혼합`

`※ t= ε이면 A → B ( 단일 생성 규칙 ), A → ε ( ε-생성규칙 )`

<br/>

<br/>

<br/>

## 2. Regular Expression (정규 표현)

**[정의 3.1] Regular expression 정의**

> - appearance of the strings을 직접 기술
> - string pattern 표현
> - 기본 요소는 φ, ε, 그리고 terminal symbol
> - e1, e2가 각각 정규 언어 L1, L2를 표현하는 정규수식이라면, 
>   - (1) (e 1)+(e 2)는 L1∪L2를 나타내는 정규수식 ( union )
>   - (2) (e 1)•(e 2)는 L1∪L2를 나타내는 정규수식 ( concatenation )
>   - (3) (e1)* *는 L1*={ε} ∪ L1 ∪ ...L1n∪⋯를 나타내는 정규수식 ( closure )
> - No other regular expressions exist

<br/>

ex)

```tex
정규수식 ab* ⇒ 언어 { abⁿ | n≥0 }
정규수식 (0+1)* ⇒ 언어 {0, 1}*
정규수식 (a+b)*abb ⇒ a,b가 반복된 후에 abb로 끝나는 string 집합
identifier의 정규수식 : letter(letter+digit)*
```

<br/>

`※축약 표기
	—(e1)+(e2) = (e1) | (e2)
	—(e1)•(e2) = (e1)(e2)
	—e1+: e1•e1*`

`※ 정규수식의 우선 순위 : 괄호 > * > •  > +`

<br/>

**[정의 3.3] Regular expression Equality **

> - **Lα=Lβ이면 α=β**
> - **L(α+β) = L(α) ∪  L(β)**
> - **L(αβ) = L(α)L(β)**
> - **L(α*) = L(α)***

<br/>

ex)

```tex
정규수식 ab* ⇒ 언어 { abⁿ | n≥0 }
정규수식 (0+1)* ⇒ 언어 {0, 1}*
정규수식 (a+b)*abb ⇒ a,b가 반복된 후에 abb로 끝나는 string 집합
identifier의 정규수식 : letter(letter+digit)*
```

