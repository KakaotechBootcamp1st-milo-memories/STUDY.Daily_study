# 생성형 챗봇에게 내 데이터를 학습시키기
## AI Model에게 내 지식을 학습시키는 2가지 방법
### 1. Fine-tunning 방식
<img width="483" alt="image" src="https://github.com/user-attachments/assets/e455b738-a446-43d9-a6ee-bb676794fe93">

- 기초 모델에 대량의 추가 데이터 반복 학습을 통해 튜닝된 새로운 모델을 만들어 사용
- 파인튜닝 데이터 샘플: https://platform.openai.com/docs/guides/fine-tuning/example-format
#### 원본 모델 A에 대량의 추가 데이터 반복 학습을 통해 튜닝된 새로운 모델 A'를 만들어 사용
https://platform.openai.com/docs/guides/fine-tuning
https://platform.openai.com/finetune/
1. 학습할 질문/답변 데이터 셋 파일을 준비(100건 이상)
<img width="440" alt="image" src="https://github.com/user-attachments/assets/9ff32617-86d9-429d-95a8-2be1bb6dfd0e">

2. OpenAI CLI로 전처리해서 CSV, TSV, XLSX, JSON -> JSONL 파일로 만듬.
```openai tools fine_tunes.prepare_data -f <LOCAL_FILE>```

3. OpenAI CLI로 fine-tuning 작업 등록
```openai api fine_tunes.create -t <TRAIN_FILE_ID_OR_PATH> -m <BASE_MODEL>```

4. 파인 튜닝된 개인 모델 ID를 사용해서 Chat GPT 사용
```
# Note: you need to be using OpenAI Python v0.27.0 for the code below to work
import openai

openai.ChatCompletion.create(
  model=“<FINE_TUNED_MODEL>”,
  messages=[
    {"role": "system", "content": "You are a helpful assistant."},
    {"role": "user", "content": "Who won the world series in 2020?"},
    {"role": "assistant", "content": "The Los Angeles Dodgers won the World Series in 2020."},
    {"role": "user", "content": "Where was it played?"}
  ]
)
```
#### 코드 레벨에서 직접 해보고싶다면?
파이토치(토치튠)
https://pytorch.org/torchtune/main/tutorials/first_finetune_tutorial.html#fine-tune-your-first-llm

라마 팩토리
https://devocean.sk.com/blog/techBoardDetail.do?ID=166098&boardType=techBlog

### 2. RAG(검색 증강 생성, Retrival-augmented Generation) 방식
<img width="445" alt="image" src="https://github.com/user-attachments/assets/5cc06f32-8ec7-482e-b54e-d9c962a9f87c">

- 사전에 지식을 벡터화해서 DB에 저장해두고 사용자의 질의에 관련된 정보를 검색하여 해당 정보가 담긴 문서들을 프롬프트를 통해 언어 모델에 함께 전달해서 답변을 생성
> 벡터화가 뭔가요..
  - 텍스트, 이미지, 소리 등의 다양한 데이터를 숫자로 이루어진 벡터로 변환하는 과정이라고 합니다.
  - 예를 들어 "고양이"라는 단어를 벡터화하면 컴퓨터는 그 단어를 고유한 숫자 배열로 표현한다고 합니다.
  - 이를 통해 컴퓨터는 단어의 의미를 비교하거나 계산할 수 있다고 합니다!
> 벡터는 크기와 방향을 가진 물리량 아닌가요..
  - 그건 고등학교나 물리학에서 배우는 유클리드 기하적 벡터를 가리키는 좁은 의미라고 합니다.
  - 여기서 말하는 벡터는 단어, 문장, 문서와 같은 텍스트 데이터의 특징을 수치적으로 표현한 다차원 공간의 점이라고 합니다.
  - 벡터화에 대해서는 아래에서 더 보겠습니다!
  <img width="127" alt="image" src="https://github.com/user-attachments/assets/7efefa23-e42b-4329-86b9-090e4aaf1d67">

  - 벡터 공간에서 점은 다음과 같이 나타나고 만약 "고양이"와 "강아지"라는 단어가 있으면 서로 유사한 의미를 가지고 있으므로 벡터 공간에서 가깝게 위치하게 된다고 합니다!
- 언어 모델에게 모르는 지식에 대한 질문을 하면 모른다고 하지만 컨닝페이퍼를 제공하면 원래 알고있었던 것처럼 대답함
<img width="607" alt="image" src="https://github.com/user-attachments/assets/5edda78f-b614-4235-aebd-69b766debc39">

<img width="435" alt="image" src="https://github.com/user-attachments/assets/914b5fc0-c76f-4cbd-b861-f3f41a8e46da">

- 사용자의 질문과 관련된 배경 지식을 벡터 유사도 검색(ANN)을 통해 벡터 DB에서 검색하고 검색된 지식을 Prompt로 사용자 질문과 함께 언어 모델에 전달하면 Context를 토대로 답변 생성
<img width="646" alt="image" src="https://github.com/user-attachments/assets/dfdc90f1-5936-46c8-8e40-325e4cb9af49">

<img width="586" alt="image" src="https://github.com/user-attachments/assets/bb5ed159-13dc-4d90-be39-4ec7685c6848">

- Context를 동적으로 가져오는 방법 -> 벡터 유사도 계산에 의한 의미론적 검색
<img width="669" alt="image" src="https://github.com/user-attachments/assets/9da8bb64-1006-4c03-ba3b-be3e11296205">

#### Embedding 지식
임베딩 벡터의 유사도 검색(ANN: Approximate Nearest Neighbors)의 원리? 의미론적 방향성!
<img width="371" alt="image" src="https://github.com/user-attachments/assets/109ac080-2bf4-46f9-9157-f3e0599ff35d">

자연어를 벡터로 바꾸는 방법?Embedding Model
https://platform.openai.com/docs/guides/embeddings/what-are-embeddings
임베딩 API 사용해보기.

자연어 문장을 임베딩 API에 던지면 1,536개 짜리 벡터 숫자 리스트가 옴
이걸 자연어 원본 문장이랑 매핑해서 같이 지식 데이터로 저장
이후 사용자 입력 자연어가 들어오면 이것도 임베딩 API에 던져서 변환
그리고 저장된 지식 데이터와 사용자 입력 자연어와의 유사도 계산을 수행
<img width="199" alt="image" src="https://github.com/user-attachments/assets/760665e7-0d71-4d79-9426-c5772a3905b3">

임베딩 시 사용되는 모델은 거대 언어모델에 비해 가볍고 싸다.(1억 토큰에 40달러)
<img width="578" alt="image" src="https://github.com/user-attachments/assets/d658b95c-a8b1-4ab1-a306-8e93bbdb1144">

## Fine-Tunning VS RAG(검색 증강 생성, Retrival-augmented Generation) 장단점 비교
### Fine-Tunning: '공부' 의미의 학습
#### 장점
- 다양한 지식에 대한 융합
- 단어의 의미, 말투, 패턴 등 학습
#### 단점
- 할루시네이션 존재
- 학습 시간과 비용 많이 소요
- 활용 지식에 대한 통제가 어려움
- 많은 양의 학습 데이터 필요

### RAG(검색 증강 생성, Retrival-augmented Generation): '단순 기억' 의미의 학습
#### 장점
- 실시간 학습, 비용 적음
- 답변에 대한 통제가 상대적으로 용이함
#### 단점
프롬프트로 전달 지식의 토큰 제한 존재
학습 데이터의 정제 필요

### 어떨 때 뭘 써야할까
결국 Production 급 Q&A 봇의 역할을 하려면 둘 다 필요
데이터 정제 + 모델 파인튜닝 + Advanced RAG Pipeline

#### Fine-Tunning: 특정 태스크에 대한 능숙함, 말투, 새로운 단어에 대한 학습
#### RAG(검색 증강 생성, Retrival-augmented Generation): 지식에 대한 단순 기억과 이를 참고한 답변 생성

# AI Agent의 이해
AI Chatbots: 질문에 대한 답변을 제공하거나 기본적인 정보 제공
AI Agents: 자율적으로 환경을 감지하고 상황에 맞게 행동을 결정하며 목표를 달성하기 위해 계획을 세우고 다양한 작업을 수행
- 환경: 현재 시간, 날씨, 위치, 온도, 국가 등
- 상황: 내 정보, 상대방 정보, 일정, 이전 기억 등

글로벌 클라우드 빅테크 들의 AI 플랫폼은 AWS - Bedrock, MS - Microsoft AI Studio, GCP - Vertex AI Studio 의 브랜딩을 가지고 있음.
최근 출시한 클라우드 기반 AI Agent Builder 제품 관련 내용

AWS - Bedrock Agent
서비스 화면: https://aws.amazon.com/ko/bedrock/agents/
문서: https://docs.aws.amazon.com/bedrock/latest/userguide/agents.html
데모: https://aistylist.awsplayer.com/

Microsoft - Microsoft Copilot Studio
서비스 화면: https://www.microsoft.com/ko-kr/microsoft-copilot/microsoft-copilot-studio
문서: https://learn.microsoft.com/ko-kr/microsoft-copilot-studio/copilot-plugins-architecture

Google Cloud Platform(GCP) - Agent Assist
서비스 화면: https://agentassist.cloud.google.com/
문서: https://cloud.google.com/agent-assist/docs/basics?hl=ko

<img width="223" alt="image" src="https://github.com/user-attachments/assets/41ba1a31-f8fe-46a7-a7c5-96138e9294e3">

모델: AI Agent와 사람이 자연어로 소통
프롬프트: AI Agent가 문제 해결 계획 수립
지식 학습: AI Agent에게 나의 지식을 기억
도구(API): AI Agent가 액션(기능)을 실행

# AI Chatbot의 이해
현재는 생성형 AI 기술 기반의 LLM을 이용한 AI Agent로 진화중

<img width="594" alt="image" src="https://github.com/user-attachments/assets/56ca6824-9417-4b15-a569-1a17f8e5cb2a">

https://arxiv.org/pdf/2309.07864.pdf
동작 예시: https://chat.openai.com/share/e/be7e1a4f-4a75-4eda-a5a0-50dd9736913d

# AI Agent와 Action의 연결
AI 에이전트에게 기존 시스템의 API 스펙을 전달하면 자동으로 연결하여 시스템과 사람이 자연어로 소통

<img width="608" alt="image" src="https://github.com/user-attachments/assets/1762ef87-cddc-4512-b17c-a7fcb615e3e4">

생성형 AI의 등장으로 AI Agent에 외부 시스템 API를 연결하는 과정이 매우 쉬워짐

<img width="608" alt="image" src="https://github.com/user-attachments/assets/eddb99c4-e462-4634-932d-503d16bfa45e">

주어진 자연어 요청을 처리하기 위해 어떤 도구를 사용해야하는지 LLM이 스스로 판단
https://chat.openai.com/share/e/0f9b9af8-b729-4d79-8599-d6e95009a164
<img width="659" alt="image" src="https://github.com/user-attachments/assets/33623a0b-587e-4f99-b7f7-ca730c5b3e38">

## LLM + 지식(RAG) = 생활백서봇

<img width="659" alt="image" src="https://github.com/user-attachments/assets/9004b107-34b3-4284-bae6-d86f5cdd3486">

답변을 제공하지 못할시 담당자를 멘션하고 #학습 태그와 함께 답변을 제공하면 답변 자동 학습

<img width="659" alt="image" src="https://github.com/user-attachments/assets/4fc8c159-50a2-4ab5-92ca-3733be2ca584">

## LLM + 지식(RAG) + 액션의 연결 = 미팅어레인지봇
미팅 어레인지 봇을 통해 좀 더 여러 AI Agent간의 액션 협업 기초 실험

<img width="659" alt="image" src="https://github.com/user-attachments/assets/709ee963-893a-4548-82c8-433797cef8e9">

## AI Agent 데모: 미팅 어레인지봇
미팅 AI Agent에게 조직 내 미팅 가능한 인원 파악해서 미팅 예약을 요청

<img width="682" alt="image" src="https://github.com/user-attachments/assets/8aff3456-077b-4ad9-8784-ee1a4163e9ce">

<img width="682" alt="image" src="https://github.com/user-attachments/assets/76feb0b3-684d-4641-87ce-762d0c3001ee">
