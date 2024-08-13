# 클라우드 컴퓨팅
## 발전 과정
###Grid Computing
- 대용량의 컴퓨팅 리소스를 필요로 하는 서비스 지원
- 인터넷 상의 모든 PC형태의 컴퓨팅 리소스 사용

###Utility Computing
- 과금 형태의 서비스로 컴퓨팅 리소스를 제공
- 전기나 수도와 같이 필요할 때마다 연결하여 사용하고 과금

###SaaS
- 서비스 제공자의 서버에 저장된 Software를 인터넷을 통해 서비스 형태로 제공
- 웹표준 개발을 통해 다양한 브라우저에서도 동일한 서비스 제공

###Cloud Computing
- 언제 어디서나, IT자원을 서비스 형태로 제공
- Software뿐만 아니라 모든 IT자원을 서비스 형태로 제공
- 기술적으로는 Thin Client를 이용한 분산 컴퓨팅을 과금 형태로는 유틸리티 컴퓨팅을 채택

## 클라우드 컴퓨팅의 모델
- 퍼블릭 클라우드 (Public Cloud)
  - CSP(Cloud Service Provider)가 제공하는 일반적인 형태의 클라우드 환경
- 프라이빗 클라우드 (Private Cloud)
  - 특정 조직을 위한 전용 클라우드 환경으로, 보안성을 강화할 수 있다.
  - 온프레미스로 구성을 할 수도 있고, CSP를 통해 호스팅을 맡길 수 있다.
  - 클라우드 환경 자체를 관리할 인력이 필요하다.
- 하이브리드 클라우드 (Hybrid Cloud)
  - 퍼블릭 클라우드와 프라이빗 클라우드를 결합하여 사용하는 형태로, 각각의 이점을 모두 활용할 수 있다.
  - 구현과 운영의 난이도가 높고, 자칫 잘못하면 각 클라우드의 관리 체계가 나뉘어져 하이브리드로서의 장점을 잃게 될 수 있다.
- 멀티 클라우드 (Multi Cloud)
  - 여러 CSP의 서비스를 혼합하여 운영하는 형태이다.
  - 서비스별로 유리한 업체를 선정하여 비용을 최적화할 수 있고, 클라우드 환경 자체에서 발생할 수 있는 위험을 분산할 수 있다.
  - 다양한 클라우드 환경으로 이루어졌으므로 관리의 어려움이 있다.
- IaaS (Infrastructure as a Service, IaaS)
  - 가상화된 컴퓨팅 자원(컴퓨팅, 스토리지, 네트워크 등)을 제공하여 사용자가 인프라를 직접 구성하고 관리할 수 있도록 제공한다.
  - ex) AWS EC2, Azure VM, GCP GCE
- PaaS (Platform as a Service, PaaS)
  - 애플리케이션을 개발, 운영하는데 필요한 플랫폼과 환경을 제공한다. 직접 인프라를 구성하거나 관리할 필요가 없어 개발에 집중할 수 있다.
  - ex) AWS Elastic Beanstalk, Azure App Services, GCP App Engine, Vercel, Heroku
- SaaS (Software as a Service, SaaS)
  - 소프트웨어 애플리케이션을 클라우드 환경을 통해 제공하며 별도의 설치, 유지보수 없이 애플리케이션을 사용할 수 있다.
  - ex) 인터넷을 통해 사용할 수 있는 대부분의 서비스
 
## 클라우드 네이터브란?
클라우드 환경의 이점을 최대한 활용하여 아키텍쳐를 설계하고 앱을 개발하여 서비스를 운영하는 방법론
### 구성 요소
#### 컨테이너
- 애플리케이션과 환경을 컨테이너로 만들어 실행 환경 간의 일관성을 보장한다.
- 컴퓨팅의 최소 자원을 컨테이너를 기준으로 하여 자원을 효율적으로 사용할 수 있다.
- 애플리케이션 환경을 경량화하여 빠른 배포가 가능하다.
#### 마이크로서비스 아키텍처(MSA, Micro Service Architecture)
- 애플리케이션을 기능을 중심으로 작은 단위의 서비스로 분할한다.
- 결합도를 낮추는 효과를 가지며, 장애가 발생하더라도 애플리케이션의 동작이 중지되지는 않는다.
- 서비스에 적합한 환경(기술스택)을 기능에 맞게 선택하여 적용할 수 있다.
#### 지속적 통합 및 배포(CI/CD, Continuous Integration/Continuous Deployment)
- 지속적 통합(CI, Continuous Integration)
  - 코드의 변경 사항을 감지하여 자동화된 파이프라인을 통해 빌드 및 테스트를 진행합니다.
- 지속적 배포(CD, Continuous Deployment)
  - 코드의 변경사항을 애플리케이션 운영 환경에 반영합니다.
- DevOps(Development + Operations)
  - 문자 그대로 개발 조직과 운영 조직의 결합
  - 분리되어 있는 두 개의 조직 사이에서 발생하던 사일로 현상을 최소화하고, 소프트웨어 개발 주기를 단축시키는 방법론
  - 이를 통해 고객에게 지속적으로 가치를 제공할 수 있다.
    - 고객의 피드백을 받아 빠르게 제품을 개선해나가는 애자일 방법론과 비슷한 흐름을 갖고 있다.
# DevOps ++
## SRE(Site Reliability Enfineering, 사이트 신뢰성 엔지니어링)
- 안정적인 서비스 운영을 지원하기 위한 방법론으로 구글에서 개발되었다.
- SRE에서는 시스템의 신뢰성과 안정성을 강조한다.
- 주요 업무 및 목적
  - 모니터링
    - 안정적인 서비스 운영을 위해 애플리케이션의 성능 및 오류 등을 모니터링하여 개발 조직과의 협업을 통해 개선한다.
  - 자동화
    - 반복적으로 수행되는 작업을 자동화하여 효율성을 높이고, 시스템 운영에 대한 부담을 줄인다.
## 플랫폼 엔지니어링
- 제품 개발 조직이 개발에 집중할 수 있도록 플랫폼을 구축하고 관리한다.
  - 여기서 플랫폼은 인프라 구축, 배포 자동화, 서비스 모니터링 등을 개발자들이 쉽게 이용할 수 있도록 추상화시킨 것을 의미한다. IDP(Internal Developer Platform)라고도 부름.
- DevOps의 최종진화라고 부르기도 한다.
- 주요 업무 및 목적
  - 제품 개발 조직의 업무 효율성 향상
    - 개발 조직에서 인프라와 다양한 도구들을 쉽게 사용할 수 있도록 추상화하여 지원하여 개발 속도를 향상 시킨다.
## 클라우드 환경에서 CI/CD 파이프라인 구성해보기
- Github
  - git을 기반으로 개발자들의 협업을 위해 분산 버전 관리를 지원해주는 서비스
- AWS Codepipeline
  - 소프트웨어를 빌드하고, 테스트하고, 배포하는 일련의 과정을 하나로 통합하고 소스 코드의 변경점을 자동으로 감지하여 자동으로 배포하는 서비스
- AWS CodeBuild
  - 소스 코드를 컴파일, 빌드하고 테스트를 실행하여 CI 서비스
  - 비슷한 도구로 Jenkins, Bamboo, Travis CI 등이 있다.
- AWS Elastic Container Registry(ECR)
  - 컨테이너 이미지를 저장하는 원격 레지스트리
- AWS Elastic Container Service(ECS)
  - 컨테이너화된 애플리케이션을 손쉽게 배포, 관리할 수 있도록 지원하는 완전 관리형 컨테이너 오케스트레이션 도구
### Github
- 이번 실습에서 파이프라인의 시작점
- https://github.com/rlatjdwn4926/ktb-repo 를 기준으로 진행
  - 뼈대 그대로 진행을 원하시면 fork 후 진행
  - 별도의 테스트용 코드를 작성하셔도 무방
- 어떤 Branch를 기준으로 진행할 것인지 확인 필수
  - 자료는 master를 기준으로 진행하였으나 기본 Branch는 main으로 생성됨
### AWS Codepipeline
<img width="654" alt="image" src="https://github.com/user-attachments/assets/2ed8f556-7c88-473e-bf0f-e20f4a22a7a9">

<img width="339" alt="image" src="https://github.com/user-attachments/assets/4a3cb764-0af8-4165-8079-49d70f762745">

- Execution mode
  - Superseded: 이전 실행이 최근 실행으로 대체됨
  - Queued: 한 번에 하나씩 실행되며, 대기열에 등록됨
  - Parallel: 대기 없이 동시에 모든 파이프라인을 실행함
- Service Role
  - 생성하는 Codepipeline이 갖게 되는 권한에 대해 정의된 IAM Role
<img width="412" alt="image" src="https://github.com/user-attachments/assets/fdcee253-12d4-4343-b1a2-a57323d01a79">

- 어떤 곳에서 코드를 가져올 것인지 선택 가능, 이번 실습에서는 Github(Version2)
<img width="296" alt="image" src="https://github.com/user-attachments/assets/a0606f33-7839-4b80-9037-37c391202b9f">

<img width="257" alt="image" src="https://github.com/user-attachments/assets/ed723fae-2477-4464-9f4e-fb04c2dfbe16">

- Connect to Github으로 생성한 Github와 연결
<img width="414" alt="image" src="https://github.com/user-attachments/assets/9de4ed6a-9892-4078-8e55-a802f2831078">

- Github에 App 설치가 정상적으로 완료되면, 아래와 같이 Repository와 Branch를 설정할 수 있음
  - Default Branch는 실습에 사용할 Branch에 맞춰서 입력
<img width="288" alt="image" src="https://github.com/user-attachments/assets/3e789067-7bcb-4cf3-8668-3e58e10b7572">

- Trigger에서는 Codepipeline이 시작되는 조건 설정
- Trigger Type
  - No Filter: 별도의 필터 없이 HEAD의 변경점을 기준으로 시작
  - Specify Filter: 다양한 조건으로 파이프라인이 시작될 수 있도록 지정 가능
  - Do not detect changes: 자동으로 파이프라인 시작을 하지 않음
- Event Type
  - Push 혹은 PR을 기준으로 파이프라인 시작 가능
- Filter Type
  - 필터를 적용할 타입을 Branch와 Tag 중에서 고를 수 있음
- Branches
  - 파이프라인이 시작되는 Branch의 조건을 지정할 수 있음


### AWS CodeBuild
<img width="307" alt="image" src="https://github.com/user-attachments/assets/5e6bb77b-7ba1-4bc6-b03a-9d1305bf9754">

<img width="257" alt="image" src="https://github.com/user-attachments/assets/e5e25334-0243-465c-93b1-9f8d2f3a22dd">

<img width="297" alt="image" src="https://github.com/user-attachments/assets/e4f84ff4-ba31-4818-ac9d-782f33189978">

- Create Project로 신규 CodeBuild 생성
- Provisioning Model
  - On Demand: 새로운 요청이 있을 때마다 필요한 리소스를 구성하여 빌드
  - Reserved capacity: 빌드에 사용할 리소스를 사전에 정의하여 운영
- Environment Image
  - 빌드 환경의 이미지를 지정할 수 있다.
- Compute
  - 컴퓨팅 리소스를 어디에서 사용할 것인지 선택할 수 있다.
  - 
<img width="759" alt="image" src="https://github.com/user-attachments/assets/09f806fb-370c-429b-b1ce-c9f4057e65cb">

- CodeBuild에서 사용된 IAM Role 생성

<img width="759" alt="image" src="https://github.com/user-attachments/assets/b0ef1dd0-617c-472d-b529-d9c4a84a9677">

- 파이프라인 정상 동작을 위해 생성 단계에서는 아래와 같이 설정

<img width="301" alt="image" src="https://github.com/user-attachments/assets/3a69aabd-0a73-49fe-86c9-fd83ebdec7bf">

<img width="347" alt="image" src="https://github.com/user-attachments/assets/b957bdf9-b661-40bc-8c22-db6784e9756a">

- 처음 생성 시도 시 위와 같은 에러 발생 후 다시 생성 버튼을 누르면 두 번째 이미지와 같이 이미 생성되었다는 에러 발생
  - 생성된 CodeBuild가 노출되지 않으므로 새로고침을 한번 진행해줘야 함
 
### AWS Codepipeline
<img width="602" alt="image" src="https://github.com/user-attachments/assets/cc8964dd-cf2b-4402-bad4-98c1a28b586f">

- Deploy는 초기 구성에는 설정하지 않고 Skip

<img width="433" alt="image" src="https://github.com/user-attachments/assets/d2b40ab0-0547-4fc8-a1f5-ae621f60a262">

- 생성이 잘 되었다면 아래 이미지와 같이 파이프라인이 최초 동작하여 빌드까지 성공된 것을 확인 가능

### AWS Elastic Container Registry(ECR)
<img width="768" alt="image" src="https://github.com/user-attachments/assets/cc3d5b2c-6822-4c34-a933-5645c7ab80ef">

<img width="384" alt="image" src="https://github.com/user-attachments/assets/d10e2cbd-467c-4cd8-95cb-1f95fde1c5ab">

<img width="769" alt="image" src="https://github.com/user-attachments/assets/64ffd11d-e205-4e5f-a703-89bc7f41b5d0">

### AWS CodeBuild
- 테스트용 빌드 명령어에서 컨테이너 이미지 빌드를 위한 명령어로 변경
```
version: 0.2
phases:
  pre_build:
    commands:
      - echo Logging in to Amazon ECR...
      - AWS_DEFAULT_REGION=ap-northeast-1 #리전에 맞게 수정
      - aws --version
      - aws ecr get-login-password --region $AWS_DEFAULT_REGION | docker login --username AWS --password-stdin 587169513591.dkr.ecr.ap-northeast-1.amazonaws.com #REPOSITORY_URI에서 repo 앞까지의 도메인
      - REPOSITORY_URI=587169513591.dkr.ecr.ap-northeast-1.amazonaws.com/ktb-repo #ECR 생성 후 발급된 URI
      - COMMIT_HASH=$(echo $CODEBUILD_RESOLVED_SOURCE_VERSION | cut -c 1-7)
      - IMAGE_TAG=${COMMIT_HASH:=latest}
  build:
    commands:
      - echo Building the Docker image...
      - docker build -t $REPOSITORY_URI:latest .
      - docker tag $REPOSITORY_URI:latest $REPOSITORY_URI:$IMAGE_TAG
  post_build:
    commands:
      - echo Pushing the Docker images...
      - docker push $REPOSITORY_URI:latest
      - docker push $REPOSITORY_URI:$IMAGE_TAG
      - echo Writing image definitions file...
      - printf '[{"name":"ktb-repo","imageUri":"%s"}]' $REPOSITORY_URI:$IMAGE_TAG > imagedefinitions.json #name에 repo
artifacts:
  files: imagedefinitions.json
```

<img width="720" alt="image" src="https://github.com/user-attachments/assets/e9570001-8331-4dd5-aab4-49d310ef5012">

- CodeBuild Project의 IAM 수정
- Service Role의 링크를 통해 이동

<img width="380" alt="image" src="https://github.com/user-attachments/assets/fb54f231-f5f3-46ef-971e-aefb7be73eef">

- 기본 IAM Role은 위와 같이 설정되어 있음

<img width="556" alt="image" src="https://github.com/user-attachments/assets/8cc95572-6d8c-455a-99e3-f746c3b11d6f">

<img width="556" alt="image" src="https://github.com/user-attachments/assets/325f2a33-be52-4865-82c3-ddaffecfdaa9">

- 빌드 과정에서 ECR 권한이 필요하기 때문에 AmazonEC2ContainerRegistryPowerUser를 추가

<img width="723" alt="image" src="https://github.com/user-attachments/assets/0cea7eff-dfe9-4412-87a7-0cfeacf0699f">

- CodeBuild 설정과 buildspec.yml을 수정하여 Git을 최신화하면 ECR에 이미지가 올라온 것을 확인 가능

### AWS Elastic Container Service(ECS)
<img width="750" alt="image" src="https://github.com/user-attachments/assets/bd17138b-9856-4a4f-a203-5b23e3a7cf0a">

<img width="374" alt="image" src="https://github.com/user-attachments/assets/62f23343-9285-46e8-a595-a68ecf69dbe6">

- Infrastructure
  - 컨테이너를 구성할 인프라 풀을 지정
  - AWS Fargate
  - Amazone EC2 Instance

<img width="456" alt="image" src="https://github.com/user-attachments/assets/14015488-e683-4255-9e7c-d7ca96974fab">

<img width="526" alt="image" src="https://github.com/user-attachments/assets/0382b283-8a3c-46db-b2a4-2162fd6d35c2">

- Compute options
  - 인프라 풀을 구성할 전략 지정
  - Capacity Provider Strategy
  - Launch Type

<img width="352" alt="image" src="https://github.com/user-attachments/assets/33d29309-5b89-4bb4-a4e9-9b7bd4abac7f">

- Application Type
  - 컨테이너를 띄울 애플리케이션 종류를 지정
  - Service: 웹 애플리케이션과 같이 오랜 시간 컴퓨팅을 쓰는 종류의 애플리케이션
  - Task: 일회성으로 실행되는 애플리케이션

- Task Definition
  - 서비스 내에서 실행될 컨테이너 스펙을 정의함
  - 첫 생성 시에는 정의된 Task Definition이 없으므로, go to Task Definition을 통해 생성

<img width="771" alt="image" src="https://github.com/user-attachments/assets/2e8b907d-ab49-4cf9-b59a-a7c80a341dbc">

<img width="402" alt="image" src="https://github.com/user-attachments/assets/0d1653e7-22ec-48ff-95ae-fd2d013de76f">

<img width="383" alt="image" src="https://github.com/user-attachments/assets/4a6f8cee-f62d-4966-98a0-11965a029198">

- Load Balancing
  - 서비스를 외부에 노출시키기 위해 로드밸런서 생성

<img width="314" alt="image" src="https://github.com/user-attachments/assets/2b8b42f7-31a9-4b91-9427-e4baa32ed174">

<img width="423" alt="image" src="https://github.com/user-attachments/assets/484ddb7b-40a2-4375-9f1d-8297a6512858">

<img width="480" alt="image" src="https://github.com/user-attachments/assets/07b71559-e5bc-4a27-b3cf-6c373c7cefb6">

- 현재 만든 웹 서비스의 경우 별도 인증서가 없으므로 HTTP(80)만 오픈

<img width="446" alt="image" src="https://github.com/user-attachments/assets/febed8c6-13b2-421e-8735-09fcdd9750fd">

- 위에서 생성한 Security Group 추가
- 이후 LB의 DNS에 접근하면 잘 접근되는 것을 확인 가능

### AWS Codepipeline
<img width="713" alt="image" src="https://github.com/user-attachments/assets/2a691bb8-3059-4a9b-b382-b57968be9f85">

<img width="635" alt="image" src="https://github.com/user-attachments/assets/99208ab1-f6a9-49e1-a3c2-a90912432ae4">

<img width="517" alt="image" src="https://github.com/user-attachments/assets/1673cca8-c721-44be-81a8-c779b92d5b3c">

<img width="541" alt="image" src="https://github.com/user-attachments/assets/1faa4c53-0e2a-40e1-9e57-9da5062347d2">

- Codepipeline 생성 단계에서 Skip했던 Deploy Stage 추가

- 파이프라인 Trigger를 위해 코드 수정 후 Push
```
// src/app.js
const express = require('express');

const app = express();

app.get('/', (req, res) => {
  res.send('Hello, KTB World!'); //해당 위치의 내용을 수정
});

app.get('/ping', (req, res) => {
  res.status(200).send('ping');
});

module.exports = app;
```

<img width="758" alt="image" src="https://github.com/user-attachments/assets/6ec0e78e-03d1-41f4-8003-44e744acb35b">

- Deploy까지 잘 수행되면 CI/CD 파이프라인 구성 완료
