# Kubernetes란?
- 대규모 분산 서버 환경에서 Container 관리를 자동화하는 유연하고 확장성 있는 오픈소스 플랫폼.
- 클라우드 제공 서비스: Google GKE, AWS EKS, MS Azure AKS 등.
- Kubernetes 애플리케이션은 클라우드에서 동일하게 동작 가능.
## Kubernetes의 주요 기능
- **스케줄링**: 다수의 컨테이너를 다수의 호스트(클러스터)에 적절하게 분산 실행.
- **상태 관리**: 원하는 상태(desired state)로 실행 상태를 유지.
- **배포 / 스케일링**: 서비스 중단 없이 자동화된 배포와 스케일링.
- **서비스 디스커버리**: 새로운 컨테이너에 접근할 수 있는 방법 제공.
- **Resource 연결 관리**: 컨테이너의 라이프 사이클에 맞춰 자원 연결.
## Kubernetes 동작 원리
- **Master & Slave 아키텍처**
  - `kube-apiserver`: 모든 요청을 받고, etcd에 저장.
  - `kube-controller-manager`: Resource 관리를 수행하는 컨트롤러들 집합.
  - `kubelet`: Worker Node에서 Node와 Pod의 상태 파악 및 실행.
  - `etcd`: 모든 오브젝트 상태를 저장하는 key/value 저장소.
  - `kube-scheduler`: 새로운 Pod의 생성을 감지하여 스케줄링.
## Declarative API (선언형 API)
- **Object와 Controller**
  - Deployment로 Object(YAML, JSON)를 제출하여 Controller가 desired state와 current state를 비교, Resource 관리.
## DKOS(Datacenter of Kakao OS) 소개
- **KaaS (Kubernetes as a Service)**
  - 카카오 개발자가 사내 프라이빗 클라우드에서 Kubernetes 클러스터를 생성하여 사용.
  - 수만 대의 서버와 수십만 개의 컨테이너를 관리.
  - 2018년부터 DKOSv3 개발 시작, 2019년 카카오택시 및 카카오톡에 적용, 2020-2021년 전사 서비스에 확대 적용.

## Kubernetes를 도입하면 좋은 점
  1. **자동 배포/실행**: 수천 대의 서버에 컨테이너화된 애플리케이션 자동 배포.
  2. **자동 복구**: Application 장애 시 다른 서버에서 자동으로 복구.
  3. **무중단 업데이트**: 서비스 중단 없이 새로운 버전으로 업데이트.
  4. **클러스터 관리**: KaaS를 이용하여 클러스터에 서버 추가/삭제 용이.

## Virtualization
- **Virtualization이란?**
  - **넓은 의미**: 컴퓨터 리소스(CPU, 메모리, 스토리지, 네트워크 등)의 추상화.
  - **좁은 의미**: 단일 컴퓨터의 리소스를 가상 머신(VM)이라 불리는 다수의 가상 컴퓨터로 분할.

- **장점**
  - 리소스 효율성: 새로운 서비스를 위해 서버를 구매할 필요 없음.
  - 관리 편의성: Infrastructure as Code(IaC) 자동화.
  - 가동 중단 시간 최소화: VM을 여러 개 두어, High Availability 구성.
  - 프로비저닝 고속화: 더 많은 컴퓨팅 리소스가 필요하면 VM을 더 생성.

## VM vs Container

- **Virtual Machines (VM)**
  - 각 VM은 별도의 운영체제(OS)를 가짐.
  - Hypervisor를 통해 호스트 OS에서 실행됨.

- **Docker Containers**
  - 동일한 OS 커널을 공유하고 프로세스 수준에서 격리.
  - 더 가벼우며 빠른 시작과 종료.

## Container
- **장점**
  - 어플리케이션과 구동 환경만을 가상화하여 프로세스로 실행.
  - 부팅 시간과 오버헤드가 적으며, 이미지가 가볍고 실행 속도가 빠름.

- **단점**
  - Kernel Panic 발생 시 모든 컨테이너가 영향을 받음.
  - 여러 대의 VM을 두어 극복.

- **격리 기술**
  - 컨테이너는 구동 환경을 격리하여 어느 환경에서도 동일하게 실행 가능.

- **Container Runtime**
  - 컨테이너를 빌드하고 실행하는 도구. 예: Docker.

## Container Orchestration
- **필요성**
  - 대용량 서비스에서 다수의 VM 및 컨테이너 관리.
  - Docker만으로는 부족한 배포, 모니터링, 서비스 검색 및 노출, 네트워크 관리 필요.

- **개발 트렌드의 변화**
  - Monolithic Architecture에서 Microservice Architecture로 변화.
  - 작은 단위로 애플리케이션을 분리하여 배포 주기가 짧아지고 관리가 용이.

## Kubernetes
- **클러스터 기반**
  - 애플리케이션 컨테이너의 위치와 실행을 자동화.
  - **Master와 Worker Nodes**:
    - Master: 클러스터 전체를 조율하는 관리자.
    - Worker Nodes: 애플리케이션을 구동하는 작업자.
  
- **Master Components**
  - kube-apiserver: API 서버
  - scheduler: 스케줄링
  - controller manager: 컨트롤러 관리
  - etcd: 상태 저장소

- **Node**
  - 애플리케이션이 실행되는 VM 또는 물리 장비.
  - kubelet 에이전트를 통해 마스터와 통신.

### 애플리케이션 배포

- **배포 과정**
  - 마스터가 애플리케이션 컨테이너를 구동하도록 지시.
  - kubelet이 컨테이너 실행 및 상태 체크 수행.

## Pod
- **Pod란?**
  - Kubernetes에서 생성, 관리, 배포 가능한 가장 작은 컴퓨팅 단위.
  - 하나 또는 여러 개의 컨테이너 그룹.
  - 동일한 호스트 내에서 네트워크와 스토리지 자원 공유.

- **장점**
  - 단일 목적의 컨테이너들을 묶어 관리.
  - pause 컨테이너를 통해 namespace 공유로 통신 가능.

- **설계 패턴**
  - 사이드카 패턴: 주요 컨테이너 옆에 보조 컨테이너 배치.
  - 엠버서더/프록시 패턴: 컨테이너 간 통신 중계.
  - 어댑터 패턴: 외부 시스템과의 호환성을 제공.
