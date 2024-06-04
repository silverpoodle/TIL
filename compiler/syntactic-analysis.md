# Syntactic Analysis (구문 분석)

- **구문 분석 (Syntactic Analysis)**: 프로그램 구조의 정확성을 확인합니다.
- **파서 (Parser)**: 구문 분석을 수행하는 구성 요소입니다.
  - **입력**: 어휘 분석기에서 나온 토큰.
  - **출력**: 중간 코드 생성기로 전달되는 구문 구조.

<br/>

<br/>

## Parsing Methods
### Derivation Tree (Parse Tree)
- **상향식 파싱 (Top-down Parsing)**: 루트 노드에서 단말 노드로 (left derivation).
- **하향식 파싱 (Bottom-up Parsing)**: 단말 노드에서 루트 노드로 (right derivation).

<br/>

### 상향식 파싱 (Top-down Parsing)

- **과정**:
  1. 시작 심볼의 첫 생성 규칙을 적용합니다.
  2. 생성된 문장 형식과 입력 문자열을 비교합니다.
  3. 불일치 시, 백트래킹하여 다음 규칙을 적용합니다.
  4. 규칙 번호를 출력하거나 sub-tree 생성합니다
  
  ```
  S → cAd
  A → ab | a                                                                           
  ```
  
  ![img](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEhk8Hsx1Yxbv9oxyiANQvax9-OaX3-y2BA5GxqiGDKBWs7RRXAoNENyh5o72vvs1VOJ8m9UCKM-qnXheTVQ2_wlIjis8OXt9Uh_W717Te1EkvrZG6v41XdZgSkLPysarrGSkk0wN9JdvZhL/s320/ss.JPG)

<br/>

<br/>

### 하향식 파싱 (Bottom-up Parsing)
- **축소 작업 (Reduce Operation)**: 생성 규칙의 우변(rhs)을 좌변(lhs)으로 대체합니다.

- 각 reduce 단계에서 sub-tree를 만듭니다

- **Shift-reduce 파싱**: 
  - **Shift**: 입력 포인터를 이동하고 입력 심볼을 스택에 푸시합니다.
  - **Reduce**: 스택의 핸들(우변과 일치하는 부분)을 좌변으로 대체합니다.
  
  ![Bottom-up or Shift Reduce Parsers | Set 2 - GeeksforGeeks](https://media.geeksforgeeks.org/wp-content/uploads/Parsing1.png)

<br/><br/>



## Output of the Parser

### 파스 트리 (Parse Tree)
- **노드**:
  - **루트 노드**: 시작 심볼.
  - **내부 노드**: 넌터미널 심볼.
  - **단말 노드**: 단말 심볼.
  
  <img src="https://github.com/silverpoodle/typora-images/blob/main/image-20240604221101801.png?raw=true" alt="image-20240604221101801" style="zoom:67%;" />

<br/><br/>

### 추상 구문 트리 (AST)

- **추상 구문 트리 (AST)**: 코드 생성에 필요한 의미 있는 구문만 포함하는 간결한 트리.

  <img src="https://github.com/silverpoodle/typora-images/blob/main/image-20240604221235766.png?raw=true" alt="image-20240604221235766" style="zoom:67%;" />

<br/><br/>



## Top-Down Parsing

- **백트래킹 (Backtracking)**: 불일치 시 규칙을 다시 적용 (시간이 많이 소요)
- **결정적 파싱 (Deterministic Parsing)**: 백트래킹 없이 수행되는 파싱, LL 문법을 통해 구현

<img src="https://github.com/silverpoodle/typora-images/blob/main/image-20240604221516959.png?raw=true" alt="image-20240604221516959" style="zoom: 67%;" />

<br/>

> no-backtracking 조건 = deterministic top-down parsin

<br/>

### 좌측 재귀와 좌측 팩토링

- **좌측 재귀 (Left-Recursion)**: 넌터미널이 좌측에 나타나는 규칙 -> 무한 루프를 유발
  - **직접 재귀**: `A → Aα`
  - **간접 재귀**: `A → Bα, B → Aβ`
- **좌측 팩토링 (Left-Factoring)**: 좌측 재귀를 피하기 위해 규칙을 재구성
  - 예제: `A → ab | ag`를 `A → aA', A' → b | g`로 변환



<br/><br/>



## Bottom-Up Parsing

- **Shift-Reduce 파싱**: 스택과 입력 버퍼를 사용하여 핸들을 찾고 축소하는 방법.

  <img src="https://github.com/silverpoodle/typora-images/blob/main/image-20240604221936301.png?raw=true" alt="image-20240604221936301" style="zoom:67%;" />

<br/>

### 핸들 가지치기 (Handle Pruning)

- **핸들 (Handle)**: 축소 과정에서 생성 규칙의 우변과 일치하는 부분 문자열.
