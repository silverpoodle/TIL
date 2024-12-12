# Large Language Model

- **지도 학습** (A -> B) 를 사용하여 다음 단어를 **반복적으로** 예측
- 글쓰기, 읽기, 채팅

<img src="https://assets-global.website-files.com/65d8ee5f025f02594c614c17/66018d221b73a4678f583607_1.webp" alt="Image 1" style="zoom: 37%;" />



<br/>

### 1. LLM 이 할 수 있는 일

- 웹 기반: ChatGPT, Bard, Bing
- SW 기반: 이메일 랑우팅, 문서 검색
- 브레인스토밍, 보도자료 작성, *프롬프트 개선*, 번역
- 교정(proofreading), 요약, 분석, 이메일 라우팅
- 고객 서비스 챗봇, 전문 챗봇, IT 서비스 챗봇
  - 내부용 챗봇으로 시작 (공개적 실수 방지)
  - Human-In-The-Loop 형태로 배포
  - 안전하다고 판단된 후에 고객에게

<br/>

### 2. LLM 주의 사항

- 지식 단절 (Cut Off): 최신 정보 없음
- Hallucinations
- 입출력 길이 제한 (최대 수천 개 단어)
- 표 형식 데이터 오류
- **비정형 데이터**에 가장 적합 (텍스트, 이미지, 오디오)
- Bias & Toxicity



<br/>

### 3. Promp Engineering



<img src="https://github.com/silverpoodle/typora-images/blob/main/prompt1.png?raw=true" alt="Image 1" style="zoom: 67%;" />



### **Principle 1: 명확하고 구체적인 지침 작성**

- Tactic 1: 구분 기호(delimiters)를 사용하여 입력의 고유한 부분을 명확하게 표시
- Tactic 2: 구조화된 출력 요청
- Tactic 3: 모델에게 조건 충족 여부를 확인하도록 요청
- Tactic 4: "Few-shot" prompting (작업을 성공적으로 완료한 사례를 제시)

<img src="https://github.com/silverpoodle/typora-images/blob/main/prompt2.jpg?raw=true" alt="Image 1" style="zoom: 20%;" />

### Principle 2: Give the model time to “think”

- Tactic 1: 작업을 완료하는 데 필요한 단계를 지정
- Tactic 2: 성급하게 결론을 내리기 전에 모델이 자체 솔루션을 내도록 지시합니다.



#### What can be done

- Summarizing
- Inferring
- Transforming
- Expanding
- Chatbot



<br/>

### 4. Chain Of Thoughts

여러 프롬프트를 함께 연결하여 **복잡한 작업을 일련의 간단한 하위 작업으로 분할**

<img src="https://github.com/silverpoodle/typora-images/blob/main/prompt3.png?raw=true" alt="Image 3" style="zoom: 80%;" />

- 프롬프트에 사용되는 token 수를 줄임
- 작업에 필요하지 않은 경우 workflow의 일부 체인을 건너뜀
- 테스트가 더 쉬움, 인간 참여형(Human-In-The-Loop)을 포함할 수 있음
- 복잡한 작업의 경우 LLM 외부에 State 를 추적
- 외부 도구(웹 검색, 데이터베이스 등) 사용