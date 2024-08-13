# 질문 정리
## 1. **인공지능 프로젝트에 대한 질문**
- **질문:** 개인 또는 팀 프로젝트에서 인공지능을 활용할 때, 주로 OpenAI API를 사용하는데, 현업에서도 그렇게 하는지 궁금하며, 인공지능 분야에 취업하기 위해 어떤 공부와 역할이 필요한지?
- **답변:**
  - **Foundation Model 제작**: 대부분 연구개발을 위해 사용되며, 석/박사 학위 및 고급 인재가 필요.
  - **일반적인 취업**: AI 모델의 활용, 데이터 분석, 모델 평가, AI 응용 개발 등에 집중.
  - **추천 학습 분야**: 텍스트, 이미지, 영상, 사운드 처리 관련 AI, RAG 파이프라인, AI 에이전트 아키텍처 등.
## 2. **클라우드 엔지니어링 문제점 및 해결**
- **문제:** 많은 클라우드 관련 문의로 개발 속도 및 근무 만족도가 저하됨. 많은 문의가 이미 존재하는 가이드 문서나 아지트에 있는 질문들에 대한 것.
- **해결 방안:** 
  - **AI 기술 활용**: 
    - 가이드 문서와 아지트 문의글을 학습시켜 AI 챗봇이 자동으로 응답하도록 시스템 구축.
    - **Fine-tuning** 및 **Embedding** 기술을 활용하여 맞춤형 답변 생성.
  - **챗봇 시연:**
    - 카카오톡 챗봇을 통해 간단한 질문에 답변.
    - 아지트에서 AI 봇이 자동으로 답변을 생성하고 추가 학습을 통해 성능 개선.
## 3. **AI 응용 개발 및 역할**
- **공통 역할:** 
  - 원활한 커뮤니케이션, 실험 설계 및 결과 분석, AI 기본 윤리 상식.
- **데이터 분석 및 처리:** 
  - Python, R 등을 사용한 프로그래밍 능력, 다양한 데이터 저장소(RDB, NoSQL, ES 등) 처리 능력.
- **모델 파인튜닝:** 
  - 머신러닝 알고리즘 이해 및 구현, 딥러닝 프레임워크(TensorFlow, PyTorch) 활용 능력.
- **모델 성능 최적화:** 
  - TensorRT, ONNX, vLLM 등 도구 사용 능력.
- **프롬프트 엔지니어링:** 
  - 효율적인 프롬프트 작성, 다양한 AI 모델과의 상호작용 경험.
- **AI 응용 개발:** 
  - 웹/모바일 애플리케이션 개발, 클라우드 서비스(AWS, GCP, Azure) 활용 능력, CI/CD 파이프라인 구축 경험.

# 사례
## 문제
- 많은 클라우드 문의로 인한 개발 속도 및 근무 만족도 저하
- 문의 중 다수가 사용자 가이드에 있고 답변 사례가 있는 내용임
## 해결
### AI 기술 활용, 클라우드 운영 이슈 분석/답변 자동화
가이드 문서와 아지트 문의글 + 답글을 학습시켜 클라우드 문의 응답 AI 챗봇을 만들어보자
1. Fine-Tunning 이용: 원본 모델에 대량의 추가 데이터 반복 학습을 통해 튜닝된 새로운 모델을 만들어 사용
2. Embedding 이용: 질문과 관련된 '지식'을 챗봇에 저장, '지식'과 '질문'을 함께 언어모델에 전달해서 자연어 답변 생성
3. 
<img width="761" alt="image" src="https://github.com/user-attachments/assets/106dd7d2-96af-4140-8301-c7ffbc774b43">

### 1. Demo(1): 카카오톡 챗봇을 통해 간편하게 단순 문의
- 큐베로 .ai-dkos{자연어} 질문
- 답변시에는 신뢰성 확보를 위해 참고 문헌의 URL 링크를 함께 첨부해서 답변
<img width="838" alt="image" src="https://github.com/user-attachments/assets/ebe2b806-42b6-4ed2-a251-c7e0438ae9c7">

### 2. Demo(2): 아지트 문의글 AI 봇 자동 답변
- AI에게 멘션해서 직접 대화도 가능
<img width="494" alt="image" src="https://github.com/user-attachments/assets/27a8b6d3-60f2-41be-b4d3-e0ac94d924d8">

1. 클라우드 운영 아지트에 사용자 문의 글이 올라오면 AI 봇의 자동 답글 생성
2. 아지트 '좋아요''싫어요'로 피드백 전달, 추가 학습에 활용 -> '싫어요'피드백 시 담당자 소환
<img width="865" alt="image" src="https://github.com/user-attachments/assets/50e6c7ad-ec92-460d-a003-856f689c72ce">

### 3. Demo(3): 실시간 학습 기능
- **실시간 학습 예시**:
  - 사용자가 챗봇에게 새로운 정보를 학습시키면, 챗봇이 그 정보를 기억하고 이후 관련 질문에 대해 응답할 수 있음.
  - 예를 들어, 챗봇에게 "데니스는 아침 6시에 일어나서 운동을 하고 삼각김밥을 먹었다"라고 학습시키면, 이후 "데니스는 아침에 뭐 먹었니?"와 같은 질문에 대해 정확히 대답할 수 있음.

- **추론 기능**:
  - 챗봇이 특정 단어가 언급되지 않았더라도, 이전에 학습한 정보로부터 추론하여 응답할 수 있음.
  - 예를 들어, "데니스는 오늘 아침에 몇 시에 일어났니?"라는 질문에, 학습된 내용을 바탕으로 6시라고 응답.

### 4. **Demo(4): 언어 모델 기본 지식 활용**
- **언어 모델의 지식 활용**:
  - 학습되지 않은 내용에 대해서도 언어 모델이 기본적으로 알고 있는 지식을 바탕으로 응답할 수 있음.
  - 예를 들어, Dockerfile을 묻는 질문에 대해, 학습된 적이 없지만 Docker에 대한 일반적인 지식을 바탕으로 답변 가능.

### 5. Demo(5): 1개 국어로만 학습시켜도 다국어 답변 가능
- 대규모 언어모델(LLM) 특성상 한국어로 학습시켜도 다국어 소통을 기본 지원
<img width="865" alt="image" src="https://github.com/user-attachments/assets/6446b7b4-96b6-45a2-ab27-c96148e8c38a">

## AI Secretary: 카카오톡, 구글 워크플레이스 코파일럿
- **AI를 활용한 작업 자동화**:
  - 사용자가 자연어로 명령을 내리면, AI가 해당 명령을 실행하고 결과를 제공.
  - 예를 들어, "OpenAI 예제를 구글 문서로 저장해줘"라는 명령을 통해 AI가 자동으로 해당 작업을 수행.

- **실제 사용 예**:
  - 사용자가 다양한 작업을 자연어로 요청하면, AI가 관련 문서를 작성하거나 데이터를 저장하는 등의 작업을 자동으로 처리.
  - 사용자는 복잡한 프로그래밍 지식 없이도 AI를 통해 업무를 효율적으로 수행할 수 있음.

# Kakao AI Platform(KAP)
<img width="856" alt="image" src="https://github.com/user-attachments/assets/d62671a0-8534-49d1-aeea-45104676a7f7">

- KAP Data : 학습에 사용
- Model Store: 데이터 저장소
- KAP Serve: 모델 서빙을 위한 프로그램
- KAP Training: 훈련과 파인튜닝 포함, 실험환경 제공, 실험환경에서 정한 GPU를 사용할 수 있는 주피터 노트북을 열어줌
- KAP Agent: 만들어진 모델에 RAG, Memory Function-Call과 같은 기능을 붙여서 서비스에 전달
<img width="1191" alt="image" src="https://github.com/user-attachments/assets/1e529d0d-18e5-4f8b-a125-ef521879d81a">

<img width="517" alt="image" src="https://github.com/user-attachments/assets/18993ea5-dd7b-4437-b2df-b9fbe7838bee">

## Data Store
<img width="1229" alt="image" src="https://github.com/user-attachments/assets/43e7cb6e-d3ae-4823-94eb-d31053a67e8c">

# 프로그램의 입력과 출력 관계를 결정하는 것
## 1. 소프트웨어 1.0: 알고리즘
- 알고리즘 개발을 통해 입력과 출력 관계를 결정
- 입력 데이터 -> 프로그램(알고리즘) -> 출력
- 장점: 입출력 간 관계가 명확히 정의되어있고 필요 연산량도 낮음
- 단점: 사람이 알고리즘을 고안해 낼 수 있는 문제만 풀 수 있음
## 2. 소프트웨어 2.0: 데이터셋으로부터 학습된 머신러닝 모델
- 학습용 데이터 -> 데이터셋 학습 -> 머신러닝 모델
- 입력 데이터 -> 프로그램(머신러닝 모델) -> 출력
- 장점: 사람이 알고리즘을 만들지 못하는 문제 해결
- 단점: 학습에 많은 비용(데이터셋, 연산량, 시간)이 소모되고 기능별 모델이 필요함, 입력과 출력 관계가 보장되지 않음
## 3. 소프트웨어 3.0: 프롬프트
- 프롬프트 = 컨텍스트 + 지시
- 프롬프트 일부인 컨텍스트를 프로그램으로 볼 수 있음
- 프롬프트(프로그램 + 입력 데이터) -> LLM(Agent) -> 출력
- 장점: 하나의 모델로 다양한 기능 수행. 머신러닝 모델 개발보다 싸고 빠름, 자연어 사용, 출력을 생성함, Reasoning + Act를 스스로 할 수 있음
- 단점: 운영 비용이 크고 의도한 출력이 나오지 않을 수 있음

# 생성현 인공지능(Generative AI)
- 기존 데이터를 학습하여 새로운 콘텐츠를 만들어내는 인공지능 기술
- 사용자가 입력(Prompt)을 제공하면 생성형 AI는 이를 바탕으로 관련된 콘텐츠 생성
<img width="1229" alt="image" src="https://github.com/user-attachments/assets/6341104d-d530-4dcc-90c3-6bb01f6a11f8">
## 동작의 이해
언어 모델에서는 텍스트를 숫자(토큰)로 변환하여 처리함
텍스트를 생성하는 생성형 AI 언어 모델을 LLM(Large Language Model)이라 함

<img width="493" alt="image" src="https://github.com/user-attachments/assets/273c2482-4df3-4af0-b54b-141239c38b58">

<img width="493" alt="image" src="https://github.com/user-attachments/assets/437d7338-189a-4784-83c9-5b9888893fdc">

이 과정을 토큰화라고 하며 주로 단어나 하위 단어 단위로 토큰을 생성함
그러나 한글 토큰을 지원하지 않는 모델에서는 아래와 같이 글자당 여러 개의 토큰으로 취급됨

<img width="590" alt="image" src="https://github.com/user-attachments/assets/5ba3f902-0c20-4bb0-bedd-9f40efc57cb4">

지금에 와서는 한글 토큰에 대한 문제가 없음

앞선 문장 맥락을 고려하여 다음 나올 단어를 학습된 확률에 의해 자동 완성

<img width="1168" alt="image" src="https://github.com/user-attachments/assets/95f48105-5c25-4683-b172-a74410c31d31">

이러한 확률 선택의 다양성을 얼마나 허용할 것인지는 Temparatire 값에 따라 설정
0에 가까우면 고정적, 1에 가까울수록 창의적 답변

<img width="730" alt="image" src="https://github.com/user-attachments/assets/9801e835-e5af-4e7c-8697-1482e628845a">

앞선 입력 전체를 고려해서 다음 토큰을 추론하기 때문에 한번에 계산할 수 있는 최대 토큰 사이즈 존재 = Context Window Size

ChatGPT로 대화를 길게 나누다보면 앞서 나눈 맥락에 대한 정보가 흐려지는 것이 그 이유
앞선 대화에서 중요한 구체적인 정보를 수동 복사해서 새로운 대화에서 다시 질문하는 것이 좋은 결과를 얻을 수 있음

<img width="1044" alt="image" src="https://github.com/user-attachments/assets/2a01c941-0cb5-4fd2-86c5-026db2f38706">

### OpenAI ChatGPT 서비스는 어떻게 만들 수 있을까?
Open AI PlayGround
Completions
#### 텍스트 자동완성 기능
본래 LLM은 텍스트 자동완성 기능
Chat은 여기에 Qustion/Answer 포맷만 입히고 지시문/질문/답변 형식의 학습을 많이 시킨 것
System, User, Assistant라는 Role을 부여해서 상황과 맥락을 통제
생성형 AI 모델은 상태가 없는 함수와 같이 동작하기 때문에 상태를 저장하지 않음
시스템 지시문 + User 질문 + AI 답변을 모델의 Context Size 제한 안에서만 생성 가능
OpenAI API를 사용하는 코드로 바꿔보면
SYSTEM: 챗봇이 지켜야할 행동 강령
USER: 유저의 입력
ASSITANT: 챗봇의 답변(이전 질문/답변 맥락을 유지하려면 매번 이전 대화를 전부 함께 전달해야함)

## 챗봇의 이해
초기 챗봇은 단순 룰 베이스(시나리오) 챗봇

<img width="929" alt="image" src="https://github.com/user-attachments/assets/8ad6fb5d-c4d4-4d28-b2d1-4518f7a6fd01">

이후 ML이 적용된 AI 챗봇은 자연어 처리(LNU) 챗봇
대화의 흐름을 시나리오로 정의하고 발화의 의도를 분류하여 파라미터와 액션을 추출하여 동작

<img width="929" alt="image" src="https://github.com/user-attachments/assets/a8e3a0ee-b9c2-4a0d-9fcd-b8a0a8719039">


자연어 처리(LNU) 챗봇 설계 예시:
[https://chanos.tistory.com/entry/AI-chatbot-Dialogflow%EB%A1%9C-%EC%BD%98%EB%8B%A4%EC%9D%B4-%EC%95%8C%EB%A6%AC%EA%B8%B0-2]

대화의 흐름을 시나리오와 인텐트, 파라미터와 액션 그리고 그 시나리오대로 사람이 플로우를 디자인하는 개념.

대화가 구성되는 의도 = 인텐트, 엔티티, 문맥(컨텍스트).

컨텍스트를 연결하는 것도, 현재 처리되는 사용자의 의도가 분류된 것 기준으로 어떤 아웃풋으로 연결한다는 플로우를 빌더에 녹여서 대화 흐름을 다 디자인하는 것.

<img width="523" alt="image" src="https://github.com/user-attachments/assets/df738d88-b878-4cd7-b4c7-261fd5919662">

## 프롬프트 엔지니어링
이미지에 있는 내용을 글로 작성해 드리겠습니다:

**프롬프트 엔지니어링**

[https://learn.deeplearning.ai/chatgpt-prompt-eng/]

OpenAI 직원과 앤드류 응 교수님이 직접 강의한 무료 공개 강의.
Jupyter Notebook을 통해 웹에서 직접 실습도 하면서 배울 수 있습니다.

### 원칙1. 명확하고 구체적인 지침을 작성하라.
#### 1) 구분 기호를 사용하여 입력을 명확하게 표시

<img width="1039" alt="image" src="https://github.com/user-attachments/assets/89575b66-78b1-4468-8f25-e4f198a03c9b">

#### 2) 구조화된 출력을 요청

<img width="1039" alt="image" src="https://github.com/user-attachments/assets/004ca60f-efc4-47b4-87b2-d9cd97ae58b1">

[https://platform.openai.com/docs/guides/structured-outputs/structured-outputs]
#### 3) 모델에게 조건이 충족되었는지 확인하도록 요청

<img width="1065" alt="image" src="https://github.com/user-attachments/assets/e23542ab-37ed-4173-b629-88efb5e3dbec">

#### 4) 퓨어샷 프롬프트(출력 샘플을 제공)

<img width="1065" alt="image" src="https://github.com/user-attachments/assets/6c2741b2-01ab-4010-b064-37aa09148866">

### 원칙 2. 모델에게 생각할 시간을 줘라
#### 1) 작업을 완료하는데 필요한 단계를 지정

<img width="1065" alt="image" src="https://github.com/user-attachments/assets/8e11d106-0c60-4d64-9a60-1ae6cf85ce7e">

#### 2) 결론을 내리기 전 모델 스스로 해결책을 찾도록 지시

<img width="1065" alt="image" src="https://github.com/user-attachments/assets/46034a3f-b551-4d0a-a83d-7edc9822a0f5">

