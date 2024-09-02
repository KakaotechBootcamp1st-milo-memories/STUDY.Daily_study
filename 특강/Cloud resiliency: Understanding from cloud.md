# Cloud resiliency: Understanding from cloud

- resiliency: 회복 탄력성

## 재난 상황 사례
- CloudStrike 사건
<img width="687" alt="image" src="https://github.com/user-attachments/assets/d58c604d-39a6-4073-a252-d8ce48b51372">

- 카카오 장애 (22년)
복구: 5시간
전체 시스템 복구: 127시간
2조8천억의 손해

## 어떻게 해결해야할까?
### 재해란?
- 장애는 시스템 내적으로 발생하는 문제로 대응이 쉬움.
- 재해는 시스템 외적인 문제로 대응이 어려움.

<img width="1024" alt="image" src="https://github.com/user-attachments/assets/7dcf8eb7-3aa6-4a58-8652-dece7ef396bf">

### 신뢰성 관점에서의 재해 발생 지점
- 인프라 (하드웨어, 네트워크, 서버 등)
- 플랫폼 (데이터베이스, OS, docker/k8s 등)
- 코드 (우리가 작성하는 코드)
- 사람, 프로세스 그리고 관습

### 클라우드 환경에서의 재해
- 온프레미스, 클라우드의 가장 큰 차이점: 가축(수만 맞으면 됨)이냐 반려 동물(이름을 하나하나 지어주고 관리함)이냐의 차이
- 온프레미스 환경에서 서버 랙 한개만 주문해도 3~6개월이 걸리고 서버 하나하나가 소중해짐
- 클라우드 서버는 스케일을 조정해서 성능을 높일 수 있음.

<img width="1024" alt="image" src="https://github.com/user-attachments/assets/8e3fb60c-e907-4922-902c-cde58ffd71f1">

<img width="1024" alt="image" src="https://github.com/user-attachments/assets/032891d6-20f4-4a2e-a1c5-3bece497626a">

- 아키텍쳐의 모든 부분에서 오류가 발생할 수 있음
- 실패하지 않는 운영환경은 없음

### 재해 관리 단계
- 예방 -> 문제가 발생하지 않도록 하는 것
- 대비 -> 문제가 발생했을 때를 대비하는 것
- 대응 -> 재해가 난 것을 일단 동작하도록 하는 것
- 복구 -> 재해가 난 것을 정상화 시키는 것
- 완화 -> 같은 문제가 다시 발생하지 않도록 하는 것

### 예방: 취약점 식별 - Chaos Engineering
- 운영환경에서 갑작스러운 장애를 견딜 수 있도록 시스템을 실험하는 분야
- 시스템에 일부러 장애를 주입해보는 것
- 자동차가 충돌 테스트하는 것이나, 휴대폰의 내구성 테스트같은 것

### 예방: 보안 가드레일
- AWS IAM
- AWS Organizations
- AWS Config
- AWS CloudTrail
- AWS ControlTower

### 대비: Observability(관측가능성) 확보

<img width="783" alt="image" src="https://github.com/user-attachments/assets/6493b7c3-76ed-402e-85a2-d508dbd87c55">

- Logging: 시스템에서 발생하는 이벤트와 활동의 상세 기록
  <img width="612" alt="image" src="https://github.com/user-attachments/assets/7a620568-27fa-4e84-a51f-43b9c8a3d631">

  - 장점
    - 상세한 컨텍스트 정보 제공
    - 복잡한 문제 해결에 유용
    - 법적 규정 준수 및 감사헤 필요한 증거 제공
  - 단점
    - 대량의 데이터 생성으로 스토리지 비용 증가
    - 분석에 시간이 많이 소요될 수 있음
    - 구조화되지 않은 데이터로 인한 분석의 어려움
- Metrics: 사스템 성능과 상태를 수치화하여 표현
  <img width="639" alt="image" src="https://github.com/user-attachments/assets/8ad5ace7-c468-405c-804a-bda26568fb0c">

  - 장점
    - 빠른 데이터 수집 및 분석
    - 시각화가 용이하여 대시보드 구성에 적합
    - 경보 설정이 쉬움
  - 단점
    - 상세한 컨텍스트 정보 부족
    - 복잡한 문제의 근본 원인 파악이 어려울 수 있음
- Tracing: 분산 시스템에서 요청의 전체 경로 추적
  <img width="582" alt="image" src="https://github.com/user-attachments/assets/df852c7b-133a-4d75-bffd-cd7947d2a2db">

  - 장점
    - 복잡한 분산 시스템 문제 해결에 효과적
    - 엔드 투 엔드 성능 분석 가능
    - 서비스 간 의존성 파악 용이
  - 단점
    - 구현 및 유지보수가 복잡할 수 있음
    - 오버헤드로 인한 성능 영향 가능성
    - 대규모 시스템에서 데이터 양이 방대해질 수 있음
- Metric을 잘할려면 통계 공부를 해라!

### 대비: Alert 확보

<img width="1005" alt="image" src="https://github.com/user-attachments/assets/5a5a70bf-0e71-48d9-9dc2-14a8d8684fc6">

### 대비: Back Up 적용

<img width="1032" alt="image" src="https://github.com/user-attachments/assets/17813dfa-6d03-4432-b8d0-b11b1bf3079c">

- 누구를 백업할거냐, 어디(온프레미스, 클라우드 등)에 백업할거냐, 얼마나 자주 백업할거냐, 얼마나 오래 데이터를 가지고 있을거냐

### 대응 vs 복구
- 대응: 재해 발생 직후 즉각적인 위험을 관리하고 피해를 최소화하는 것
- 복구: 대응 이후부터 중장기적 기간으로 정상적인 비즈니스 운영 상태로 돌아가는 것
- 모의 장애 훈련
  <img width="894" alt="image" src="https://github.com/user-attachments/assets/d49defc6-41af-446e-b02c-aaf044fa4374">

### 완화
- 목적
  - 위험 감소
  - 복원력 강화
  - 비용 절감
  - 비즈니스 연속성 보장
  - 규정 준수
  - 위험 인식 제고
- 시점
  - 사전 예방적
  - 재해 발생 후
  - 계획 단계
  - 기술 변화에 따른 대응
  - 규제 변화에 따른 대응
 
### 완화: Poka-Yoke 적용
<img width="648" alt="image" src="https://github.com/user-attachments/assets/446abd49-8738-475b-9caf-90fc58340762">

- 포카 요케: 품질 관리 측면에서 실수를 방지하도록 행동을 제한하거나 정확한 동작을 수행하게끔 하도록 강제하는 여러 제한점을 만들어 실패를 방지하는 방법을 말하는 용어

### 재해 발생을 줄이는 방법
- 가장 중요한 것은 내재화

# QnA
- 분산시스템은 좋은 방법이긴 하지만 분산하는 만큼 재해가 발생할 수 있는 지점이 많아진다.
- 아키텍쳐 설계를 할 때 안티패턴을 공부하면 좋지만 설계에 대한 이유가 있으면 된다. 제일 나쁜건 내가 이렇게 해왔으니까 계속 똑같이 하는 것
