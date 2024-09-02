<img width="443" alt="image" src="https://github.com/user-attachments/assets/ea5dce21-817e-4e22-8788-6ed7e6909a43"><img width="623" alt="image" src="https://github.com/user-attachments/assets/dfdccead-b8b5-44b6-9e54-c13fb2a5e2df"><img width="623" alt="image" src="https://github.com/user-attachments/assets/4f476f95-0b1a-4b2d-b49d-3c19a08086dc">

# Marp 
## Marp VS Code
1. VS Code 확장 마켓플레이스에서 'Marp for VS Code' 설치
2. Markdown 파일 생성 (.md 확장자)
3. 파일 상단에 marp: true 디렉티브 추가
4. 마크다운으로 슬라이드 내용 작성
5. VS Code의 미리보기 기능으로 실시간 확인
6. 원하는 형식(HTML, PDF, PPTX)으로 내보내기

## Markdown 개요
- 일반 텍스트 기반의 경량 마크업 언어
- 2004년 존 그루버(John Gruber)가 만듦
- 읽기 쉽고 쓰기 쉬운 plain text 포맷을 사용
- HTML 등 다양한 출력 형식으로 변환 가능

## Markdown의 장점
1. 간단하고 배우기 쉬움
2. 다양한 플랫폼에서 지원
3. 텍스트 에디터만으로 작성 가능
4. 버전 관리 시스템과 호환성 좋음
5. 다양한 출력 형식으로 변환 가능

## Marp 개요
- Markdown으로 프레젠테이션을 만드는 도구
- Markdown As a Representation of Presentation의 약자
- 2016년 Yuki Hattori가 개발
- 간단한 Markdown 문법으로 슬라이드 제작 가능
- VS Code 확장 프로그램으로 사용 가능

## Marp의 장점
1. Markdown의 간결함과 가독성 유지
2. 코드 하이라이팅 지원
3. 테마 커스터마이징 가능
4. PDF, PPTX 등 다양한 형식으로 내보내기 가능
5. 버전 관리 시스템과의 뛰어난 호환성
6. 슬라이딩 등 발표 자료도 다양함

## Marp 사용법
### 기본 문법
- '---'로 슬라이드 구분
- '#'으로 제목 수준 지정
- '-'나 '1.'로 목록 생성
- '```'로 코드 블록 생성

### 추가 기능
- 이미지 삽입 및 크기 조절
- 배경 이미지 설정
- CSS를 통한 스타일 커스터마이징
- 수식 입력 지원 (KaTeX)

### Marp 슬라이드 내보내기
1. Markdown 파일 열기: Marp로 작성된 .md 파일을 엽니다.
2. 명령 팔레트 열기: Ctrl+Shift+P (Windows/Linux) 또는 Cmd+Shift+P (Mac)
3. Export 명령 실행:
   * "Marp: Export Slide Deck" 입력 후 선택
4. 형식 선택: PDF, PPTX, HTML 등 원하는 형식 선택
5. 저장 위치 지정: 파일 이름과 저장 위치 선택 후 저장
6. 완료: 선택한 형식으로 슬라이드가 Export 됩니다!

팁: VSCode 우측 상단의 "Preview" 버튼으로 미리보기 가능

### Marp 디렉티브
- 전역 디렉티브: 문서 상단에 작성

```
marp: true
theme: default
paginate: true
```

- 로컬 디렉티브: 개별 슬라이드에 적용
```
<!-- _class: section_title -->
<!-- _backgroundColor: yellow -->
<!-- _color: red -->
```

### 이미지 삽입
```
![width:500px](https://example.com/image.jpg)

![height:300px](https://example.com/another-image.jpg)

![width:200px height:150px](https://example.com/resized-image.jpg)

![bg](https://example.com/background-image.jpg)
```

### Claude 사용 에시

<img width="443" alt="image" src="https://github.com/user-attachments/assets/71c205dc-1c63-474e-af14-b03a4729146e">

```
- 개구리 갈비찜 레시피를 설명하는 발표 자료를 만들어보자
- Marp를 이용해서 생성한다고 가정해줘
- 10장 정도로 만들어주고 1페이지는 제목, 2페이지에는 목차를 넣어서 구성해줘
```

- 결과를 md 파일로 저장 후 vsCode에서 열기

<img width="674" alt="image" src="https://github.com/user-attachments/assets/238b58fe-7dff-411d-9495-4bafcfc090c6">

# Mermaid
## Mermaid 개요
- 텍스트 기반의 다이어그램 생성 도구
- Markdown과 유사한 문법 사용
- 다양한 종류의 다이어그램 지원
- 브라우저에서 직접 렌더링 가능

## Mermaid의 장점
1. 코드로 다이어그램 생성 가능
2. 버전 관리 용이
3. 다양한 플랫폼과 통합 가능
4. 빠른 프로토타이핑 지원
5. 자동 레이아웃 기능

## 지원 다이어그램 종류
1. 순서도 (Flowchart)
2. 시퀀스 다이어그램 (Sequence Diagram)
3. 클래스 다이어그램 (Class Diagram)
4. 상태 다이어그램 (State Diagram)
5. 간트 차트 (Gantt Chart)
6. 파이 차트 (Pie Chart)
7. ER 다이어그램 (Entity Relationship Diagram)

## 다이어그램 예시
```
sequenceDiagram
participant Application
participant FileSystem
participant OtherTask
Application-->>FileSystem: Initiate Read File
FileSystem-->>Application: Acknowledge
Application-->>OtherTask: Perform Other Task
Note right of FileSystem: File I/O operation
FileSystem-->>Application: Notify Data Ready
Application-->>FileSystem: Retrieve Data
FileSystem-->>Application: Return Data
Application-->>Application: Process Data
```

<img width="300" alt="image" src="https://github.com/user-attachments/assets/ccc51b95-ea10-441c-8c93-0226ca4d47cc">


```
classDiagram
direction TB
class ChatbotDev["[단독형 미션]<br />지능형 고객 지원 챗봇 시스템 개발"] {
  생성형 AI 적용
  사용자 인터페이스 설계
  대화 흐름 관리
  고객 대응 스킬
  창의적 문제 해결
}
...
class CICDPipeline["[연계형 미션]<br />CI/CD 파이프라인 구성"] {
  자동화 배포
  지속적 통합
  코드 품질 유지
  효율성 향상
  운영 관리
}

ChatbotDev --> CollaborationSetup
ChatbotDev --> RedisDeployment
RedisDeployment --> CICDPipeline
ChatbotDev --> DataPreparation
DataPreparation --> RAGIntegration
```

<img width="314" alt="image" src="https://github.com/user-attachments/assets/9287a627-51a6-40d8-a262-e15000b86c81">

# Marp에서 Mermaid 사용하기
- 마크다운 파일 최하단에 아래 코드 추가하기
- 또는 관련 Extension 설치하기 (추천하지 않음) -> 충돌이 일어날 때도 있음

```
<script src="https://cdn.jsdelivr.net/npm/mermaid@10.9.1/dist/mermaid.min.js"></script>
<script>
  mermaid.initialize({
    startOnLoad: true,
    securityLevel: "loose",
    htmlLabels: true
  });
  window.addEventListener('vscode.markdown.updateContent', function() { mermaid.init() });
</script>
```

## 사용해보기

<img width="900" alt="image" src="https://github.com/user-attachments/assets/a27bcdc7-2791-47b7-9202-c6fedea34b93">

- 스크립트
```
조리 과정에 대한 mermaid flow chart를 그려줘.
```

<img width="690" alt="image" src="https://github.com/user-attachments/assets/e467c9ec-a085-433e-ac90-17fb685fb8f8">

# SVG를 이용한 이미지 생성
## SVG란?
- Scalable Vector Graphics의 약자
- XML 기반의 2차원 벡터 그래픽 파일 형식
- 웹 표준 기술로, 모든 주요 웹 브라우저에서 지원
- 텍스트 기반 형식으로 검색 엔진 최적화(SEO)에 유리
- 수학적 표현으로 이미지를 정의하여 무한 확대/축소 가능

## SVG의 장점
1. 확장성: 품질 손실 없이 크기 조절 가능
2. 편집 용이성: 텍스트 에디터로 직접 수정 가능
3. 작은 파일 크기: 복잡한 이미지도 상대적으로 작은 용량
4. 애니메이션: CSS나 JavaScript로 동적 효과 구현 가능
5. 접근성: 텍스트 기반이라 스크린 리더 지원 우수
6. 스타일링: CSS를 이용한 스타일 적용 가능

## SVG 활용 사례 및 예시
웹 디자인
- 로고 및 아이콘 제작
- 인포그래픽 및 데이터 시각화
- 반응형 웹 디자인의 이미지 요소

기술 문서
- 다이어그램 및 플로우차트 생성
- 기술 도면 및 설계도 작성

애니메이션
- 인터랙티브 웹 요소 제작
- UI/UX 애니메이션 구현

특징
- 간단한 코드로 복잡한 그래픽 표현 가능
- 속성 변경만으로 쉽게 스타일 조정 가능

```html
<svg width="100" height="100">
  <circle cx="50" cy="50" r="40" stroke="green" stroke-width="4" fill="yellow" />
</svg>
```

결과
- 노란색으로 채워진 원
- 둘레는 녹색 선으로 표시
- 중심점 (50,50), 반지름 40px

## SVG vs 래스터 이미지
### SVG (벡터 그래픽)
- 확장 시 품질 유지
- 파일 크기 작음 (단순한 이미지의 경우)
- 복잡한 이미지에서는 성능 저하 가능

### 래스터 이미지 (PNG, JPEG 등)
- 확장 시 품질 저하
- 복잡한 이미지나 사진에 적합
- 파일 크기가 상대적으로 큼

### 선택 기준
- 로고, 아이콘: SVG 선호
- 사진, 복잡한 이미지: 래스터 이미지 선호
- 웹 성능과 사용자 경험을 고려하여 선택

## AI를 통한 SVG 생성
### 장점
1. 빠른 프로토타이핑: 신속하게 아이디어를 시각화
2. 코드 생성 용이: SVG 코드를 직접 작성하는 번거로움 감소
3. 다양한 스타일 실험: 다양한 디자인 옵션을 쉽게 탐색
4. 학습 도구: SVG 문법과 구조에 대한 이해도 향상
5. 접근성: 디자인 전문가가 아니어도 기본적인 그래픽 제작 가능
6. 커스터마이징: 생성된 코드를 기반으로 쉽게 수정 및 개선 가능

### 단점
1. 정확성 한계: 복잡한 디자인이나 특정 스타일 구현에 제한
2. 창의성 제한: AI의 출력은 학습된 데이터에 기반하여 제한적일 수 있음
3. 저작권 문제: 생성된 이미지의 독창성과 저작권에 대한 불확실성
4. 일관성 부족: 여러 번의 요청에서 동일한 결과를 얻기 어려울 수 있음
5. 최적화 부족: 생성된 SVG 코드가 항상 최적화되어 있지 않을 수 있음
6. 컨텍스트 이해 한계: 브랜드 아이덴티티나 특정 컨텍스트 반영에 한계

<img width="664" alt="image" src="https://github.com/user-attachments/assets/621fa2b7-d6c5-4818-9f6c-ddaa80085c15">

### 효과적인 활용 방법
1. 초기 아이디어 구상 단계에서 활용
2. 기본 템플릿으로 사용 후 수동으로 세부 조정
3. SVG 구조 학습 및 이해를 위한 도구로 활용
4. 간단한 아이콘이나 로고의 빠른 프로토타이핑
5. PPTX 에 가져가서 편집도 가능
6. Adobe Illustrator 등 벡터 이미지 저작도구에서도 수정 가능
7. SVG 파일을 구해서 그것을 주고 수정하게 만드는 법

# Marp 슬라이드 디자인 커스터마이징
## 전체 슬라이드 스타일 변경
```
/* 전체 슬라이드에 적용 */
section {
  background-color: #f5f5f5;
  font-family: 'Arial', sans-serif;
  color: #333;
}
```
- `section`: Marp의 각 슬라이드를 나타내는 선택자
- 배경색, 글꼴, 텍스트 색상 등을 일괄 변경 가능

## 제목 스타일 수정
```
/* 제목 스타일 */
h1 {
  color: #0066cc;
  border-bottom: 2px solid #0066cc;
  padding-bottom: 10px;
}

h2 {
  color: #009933;
}
```
- `h1`, `h2`: 각각 대제목과 중제목을 나타냄
- 색상, 밑줄, 패딩 등으로 강조 효과 부여

## 글머리 기호 및 번호 목록 스타일
```
/* 글머리 기호 목록 */
ul {
  list-style-type: square;
  color: #666;
}

/* 번호 목록 */
ol {
  list-style-type: lower-alpha;
  color: #666;
}
```
- `ul`: 순서 없는 목록 (글머리 기호)
- `ol`: 순서 있는 목록 (번호)
- 목록 스타일과 색상 변경 가능

## 이미지 스타일링
```
/* 이미지 스타일 */
img {
  border: 3px solid #ddd;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0,0,0,0.1);
}
```
- 이미지에 테두리, 둥근 모서리, 그림자 효과 적용
- `border-radius`로 모서리 둥글기 조절
- `box-shadow`로 그림자 효과 추가

## 코드 블록 스타일링
```
/* 코드 블록 스타일 */
pre {
  background-color: #f0f0f0;
  border-left: 5px solid #0066cc;
  padding: 10px;
  font-family: 'Courier New', monospace;
}
```
- `pre`: 코드 블록을 나타내는 태그
- 배경색, 왼쪽 테두리, 패딩으로 강조
- 고정폭 글꼴 사용으로 가독성 향상

## 특정 슬라이드 스타일링
```
/* 특정 슬라이드 스타일 */
section.lead {
  background-color: #0066cc;
  color: white;
  text-align: center;
}

section.lead h1 {
  border: none;
  font-size: 2.5em;
}
```
- `section.lead`: 특정 클래스가 적용된 슬라이드
- 배경색, 텍스트 색상, 정렬 등 변경
- 제목 스타일도 개별적으로 조정 가능

## 페이지 번호 스타일링
```
/* 페이지 번호 스타일 */
section::after {
  content: attr(data-marpit-pagination) '/' attr(data-marpit-pagination-total);
  font-size: 0.8em;
  position: absolute;
  bottom: 10px;
  right: 10px;
  color: #888;
}
```
- `section::after`: 각 슬라이드 뒤에 추가되는 가상 요소
- 페이지 번호 표시 및 스타일링
- 위치, 크기, 색상 등 조정 가능

## 스크립트 예시
```
"Marp 슬라이드에 쓸 수 있는 세로로 1/2로 분할되어 있고 우측은 또 가로로 1/2로 분할된 flexbox 기반의 html을 출력시켜줘. 배경색은 연한 회색으로 표현해줘."
```
- 결과 코드
```
<div style="display: flex; height: 100%; background-color: #f0f0f0; gap: 20px; padding: 20px;">
  <div style="flex: 1; border: 1px solid #ccc; padding: 20px;">

### 왼쪽 영역
- 텍스트
  </div>
  <div style="flex: 1; display: flex; flex-direction: column; gap: 20px;">
    <div style="flex: 1; border: 1px solid #ccc; padding: 20px;">
    
### 오른쪽 상단
- 텍스트
    </div>
    <div style="flex: 1; border: 1px solid #ccc; padding: 20px;">
    
### 오른쪽 하단
- 텍스트
    </div>
  </div>
</div>
```

- 결과
<img width="623" alt="image" src="https://github.com/user-attachments/assets/3d4eebae-0e16-4383-8c7b-86c89feb39fb">

## 스크립트 예시 2
```
"해커톤에 참여한 6명의 팀원 소개를 위해 사진, 이름, 소속, 역할, 느낌점을 담을 수 있는 Marp 슬라이드 레이아웃을 HTML flexbox로 잡아줘."
```
- 결과 코드
```
<div style="display: grid; grid-template-columns: repeat(3, 1fr); grid-template-rows: repeat(2, 1fr); gap: 20px; height: calc(100% - 40px);">
  <div style="display: flex; flex-direction: column; background-color: #fafafa; border: 1px #eee solid; border-radius: 10px; padding: 10px; box-shadow: 0 4px 6px rgba(0,0,0,0.1);">
    <img src="/api/placeholder/150/150" alt="팀원 1" style="background-color: #ccc; width: 80px; height: 80px; border-radius: 50%; align-self: center; object-fit: cover;">
    <h3 style="margin: 10px 0 5px; text-align: center; font-size: 1em;">이름</h3>
    <p style="margin: 0 0 5px; text-align: center; color: #666; font-size: 0.8em;">소속</p>
    <p style="margin: 0 5px; text-align: center; font-weight: bold; font-size: 0.9em;">역할</p>
    <p style="margin: 0; font-size: 0.8em; flex-grow: 1; overflow-y: auto;">느낀점: Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
  </div>

  ...
  
  <div style="display: flex; flex-direction: column; background-color: #fafafa; border: 1px #eee solid; border-radius: 10px; padding: 10px; box-shadow: 0 4px 6px rgba(0,0,0,0.1);">
    <img src="/api/placeholder/150/150" alt="팀원 6" style="background-color: #ccc; width: 80px; height: 80px; border-radius: 50%; align-self: center; object-fit: cover;">
    <h3 style="margin: 10px 0 5px; text-align: center; font-size: 1em;">이름</h3>
    <p style="margin: 0 0 5px; text-align: center; color: #666; font-size: 0.8em;">소속</p>
    <p style="margin: 0 5px; text-align: center; font-weight: bold; font-size: 0.9em;">역할</p>
    <p style="margin: 0; font-size: 0.8em; flex-grow: 1; overflow-y: auto;">느낀점: Lorem ipsum dolor sit amet, consectetur adipiscing elit.</p>
  </div>
</div>
```
- 결과

<img width="623" alt="image" src="https://github.com/user-attachments/assets/46f28783-1165-4862-ba47-381cbf99abd5">

