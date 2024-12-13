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





<br/>

### 5. Memory

**거대언어모델**과 상호 작용할 때 당연히 **모델은 이전에 말한 내용이나 이전 대화를 기억하지 못함**

-> 대화의 이전 부분을 기억하고 이를 언어 모델에 공급하여 상호 작용할 때, 대화 흐름을 가질 수 있도록 하는 **메모리**

`동시에 여러 개의 메모리를 사용할 가능!`

**ConversationBufferMemory**

- 이 메모리를 사용하면 메시지를 저장할 수 있으며, 변수에서 메시지를 추출

**ConversationBufferWindowMemory**

- 이 메모리는 해당 시간 동안의 대화 상호 작용 목록을 유지, 마지막 K개 상호작용만 사용

**ConversationTokenBufferMemory**

- 이 메모리는 메모리의 최근 상호 작용 버퍼를 유지하고, 상호 작용 수 대신 토큰 길이를 사용하여 상호 작용 플러시 시기를 결정

**ConversationSummaryBufferMemory**

- 이 기억은 시간이 지남에 따라 대화의 요약을 생성

**Vector data memory**

- 대화 또는 다른 곳의 텍스트를 벡터 데이터베이스에 저장하고 가장 관련성이 높은 텍스트 블록을 검색

**Entity memories**

- LLM을 사용하여, 특정 엔터티에 대한 세부 정보를 기억

<br/>

### 6. Chains

Chain은 일반적으로 LLM, **대규모 언어 모델을 프롬프트와 결합**하며, 이 빌딩 블록을 사용하면, 이러한 빌딩 블록을 함께 배치하여 텍스트나 기타 데이터에 대한 일련의 작업을 수행 가능

#### SequentialChain

한 체인의 출력이 다음 체인의 입력인 여러 체인을 결합

1. SimpleSequencialChain : Single input/output
2. SequentialChain : multiple inputs/outputs

<img src="https://nbviewer.org/github/junji64/LangChain/blob/main/SC.PNG" alt="Image 3" style="zoom: 60%;" />



#### Router Chain

해당 입력이 정확히 무엇인지에 따라 **입력을 적절한 체인으로 라우팅** 

<img src="https://nbviewer.org/github/junji64/LangChain/blob/main/RC.PNG" alt="Image 3" style="zoom: 60%;" />





<br/>

### 7. QnA over Documents

**문서에 관한 질문에 답할 수 있는 시스템**

PDF 파일이나 웹 페이지 또는 일부 회사의 인트라넷 내부 문서 컬렉션에서 추출된 텍스트가 주어지면, LLM을 사용하여 해당 문서의 내용에 대한 질문에 답하여 사용자가 더 깊이 이해하고 얻을 수 있도록 도울 수 있거나, **필요한 정보에 접근**
**언어 모델을 원래 훈련되지 않은 데이터와 결합**하기 시작하기 때문에 정말 강력합

<br/>

#### Embedding

임베딩은 텍스트 조각에 대한 숫자 표현 생성, **이 숫자 표현은 지나간 텍스트 조각의 의미를 포착**
*유사한 내용을 가진 텍스트 조각은 유사한 벡터*를 가짐, 이를 통해 벡터 공간의 텍스트 조각을 비교

<img src="https://nbviewer.org/github/junji64/LangChain/blob/main/Embedding-1.png" alt="Image 3" style="zoom: 100%;" />

<img src="https://nbviewer.org/github/junji64/LangChain/blob/main/Embedding-2.png" alt="Image 3" style="zoom: 100%;" />



#### Vector Database

**터 데이터베이스**는 이전 단계에서 생성한 이러한 **벡터 표현을 저장**
들어오는 문서에서 나오는 텍스트 덩어리로 채움 ->  큰 문서가 수신되면 먼저 이를 더 작은 덩어리

<img src="https://nbviewer.org/github/junji64/LangChain/blob/main/VectorDB.png" alt="Image 3" style="zoom: 100%;" />



<img src="https://nbviewer.org/github/junji64/LangChain/blob/main/VectorDB.png" alt="Image 3" style="zoom: 100%;" />

<img src="https://nbviewer.org/github/junji64/LangChain/blob/main/VectorDB2.png" alt="Image 3" style="zoom: 80%;" />



#### Other

 **1. Map_reduce**: 모든 청크를 가져와 질문과 함께 언어 모델에 전달하고 응답을 받은 다음 다른 언어 모델 호출을 사용하여 **모든 개별 응답을 최종 답변으로 요약**

- **개별 질문을 동시에 수행할 수 있기 때문에 매우 강력**

- 하지만 **훨씬 더 많은 대화가 필요**

  

**2. Refine**: 많은 문서를 반복하는 데에도 사용. 

- **이전 문서의 답변을 바탕으로 작성**, 이는 정보를 결합하고 시간이 지남에 따라 답변을 구축
- **일반적으로 답변이 길어짐
- ** **호출이 독립적이지 않기 때문에 속도 느림**.

**3. Map_rerank**": 점수를 반환하도록 요청,  **가장 높은 점수를 선택**합니다. 

- 모든 호출은 독립적

<img src="https://nbviewer.org/github/junji64/LangChain/blob/main/Map.png" alt="Image 3" style="zoom: 80%;" />



<br/>

### 8. RAG