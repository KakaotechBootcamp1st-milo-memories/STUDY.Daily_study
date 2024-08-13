# 강의자: 홍석용(dennis.hong)
# Cgroup
Cgroup(Control Group)은 리눅스 커널에서 프로세스와 자원을 관리하기 위한 메커니즘
Cgroup v2는 Cgroup v1의 단점을 개선하고 더 일관된 인터페이스 제공을 위한 최신 버전

<img width="640" alt="image" src="https://github.com/user-attachments/assets/5c4e73d7-7d70-4f31-8a6c-a5c687dba849">

<img width="640" alt="image" src="https://github.com/user-attachments/assets/e5ef4be4-310a-456a-89a3-357717e02874">

> 출처: https://dennis.k8s.kr/10 [데니스의 구름짓는 스터디:티스토리]

## v1 주요 특징
### 단일화된 계층 구조
cgroup v2는 단일한 계층 구조를 사용하여 모든 컨트롤러를 통합하며 cgroup v1에서 발생할 수 있는 여러 계층 구조로 인한 복잡성을 줄여줌
### 일관된 인터페이스
cgroup v2는 더 일관된 인터페이스를 제공, 모든 컨트롤러는 유사한 방식으로 동작하며, 일관된 파일과 디렉토리 구조를 가짐
### 통합된 리소스 관리
메모리, CPU, IO 등 다양한 자원을 통합적으로 관리할 수 있으며 리소스 관리가 더 직관적이고 효율적
### cgroup 컨트롤러
cgroup v2는 여러 컨트롤러를 지원함. 예를 들어, cpu, memory, io 등의 컨트롤러가 있으며 각 컨트롤러는 특정 자원을 제어하는 데 사용됨

## v1, v2 주요 특징 비교
### 단일 계층 구조
v1: 각 리소스 컨트롤러(CPU, 메모리 등)가 독립적인 계층 구조를 가짐
v2: 모든 컨트롤러가 단일 통합 계층 구조를 공유
### 내부 프로세스 규칙
v1: 계층 구조의 모든 레벨에 프로세스 존재 가능
v2: 리프 노드에만 프로세스 존재 가능, 이는 리소스 관리를 더 예측 가능하게 만듦
### 리소스 컨트롤러 구성
v1: 각 컨트롤러를 개별적으로 마운트하고 구성
v2: 단일 마운트 포인트로 모든 컨트롤러 관리
### 향상된 성능과 확장성
v2: 더 효율적인 리소스 관리와 모니터링 제공
### 일관된 API
v2: 모든 컨트롤러에 대해 더 일관된 인터페이스 제공
### 개선된 프레스 컨트롤
v2: 메모리 프레스와 같은 새로운 기능 도입
### 향상된 자원 분배
v2: 더 공정하고 효율적인 리소스 분배 메커니즘 제공
### 보안 강화
v2: 일부 취약점 해결 및 보안 기능 강화
### 실제 사용에서의 주요 차이점:
파일 시스템 구조가 변경되어 /sys/fs/cgroup/ 아래에 모든 컨트롤러가 통합됨
리소스 제한 설정 방식이 변경됨 (예: memory.limit_in_bytes 대신 memory.max 사용)
일부 설정 파일의 이름과 포맷이 변경됨

## 예시
```
# 새로운 cgroup을 생성
mkdir /sys/fs/cgroup/my_cgroup

# CPU 사용 제한 설정
echo 50000 > /sys/fs/cgroup/my_cgroup/cpu.max

# 메모리 사용 제한 설정
echo 100M > /sys/fs/cgroup/my_cgroup/memory.max

# 프로세스를 cgroup에 추가
echo $$ > /sys/fs/cgroup/my_cgroup/cgroup.procs
# 출처: https://dennis.k8s.kr/10 [데니스의 구름짓는 스터디:티스토리]
```
$$는 셸 스크립트에서 현재 실행 중인 셸 프로세스의 PID(Process ID)를 나타내는 특수 변수
이를 통해 스크립트 내에서 현재 프로세스의 ID를 쉽게 참조할 수 있음

이 예시는 새로운 cgroup을 생성하고, 해당 cgroup에 CPU와 메모리 사용 제한을 설정한 후, 현재 쉘 프로세스를 해당 cgroup에 추가하는 과정을 보여줍니다.
cgroup v2는 리소스 관리와 프로세스 격리를 보다 효율적이고 일관되게 만들기 위해 설계된 최신 메커니즘입니다. 이는 컨테이너화된 환경에서 특히 유용하며, Docker와 Kubernetes와 같은 도구에서 널리 사용됩니다.

# Namwspace
리눅스의 네임스페이스(namespace)는 서로 다른 프로세스가 다른 자원들을 독립적으로 사용할 수 있게 해주는 기능
## 주요 자원
### Mount Namespace (mnt)
파일 시스템 마운트를 독립적으로 관리할 수 있게 하며 이를 통해 각 컨테이너나 프로세스가 서로 다른 파일 시스템 뷰를 가질 수 있음
### Process ID Namespace (pid)
프로세스 ID 번호를 독립적으로 관리할 수 있으며 이를 통해 하나의 네임스페이스에서 PID 1인 프로세스가 다른 네임스페이스에서는 다른 PID로 보일 수 있음
### Network Namespace (net)
네트워크 장치, IP 주소, 포트 등을 독립적으로 관리할 수 있으며 이를 통해 각 네임스페이스가 자신만의 네트워크 스택을 가질 수 있음
### Inter-process Communication Namespace (ipc)
메시지 큐, 세마포어, 공유 메모리 등의 IPC 자원을 독립적으로 관리할 수 있으며 이를 통해 서로 다른 네임스페이스 간의 IPC 충돌을 방지할 수 있음
### UTS Namespace (uts)
호스트 이름과 도메인 이름을 독립적으로 관리할 수 있으며 이를 통해 각 네임스페이스가 자신만의 호스트 이름과 도메인 이름을 가질 수 있음
### User Namespace (user)
사용자와 그룹 ID를 독립적으로 관리할 수 있으며 이를 통해 각 네임스페이스가 다른 사용자와 그룹 ID 맵핑을 가질 수 있으며, 보안성을 높일 수 있음
### Control Group Namespace (cgroup)
컨트롤 그룹을 독립적으로 관리할 수 있으며 이를 통해 네임스페이스마다 서로 다른 리소스 제한을 설정할 수 있습니다.

# 컨테이너 사용 팁
## docker container 실행
docker run을 하면 실행한 cmd가 init 프로세스가 되므로 해당 cmd가 종료되면 컨테이너도 종료됨
컨테이너 하나에 여러개의 프로세스를 올리면 문제점: init 프로세스가 종료되면 다 죽는다.

최소 실행시에는 run, 기존 돌고있는 컨테이너에 추가 실행은 exec, 입력 필요한 터미널 실행시에는 -it
<img width="464" alt="image" src="https://github.com/user-attachments/assets/0d0fa7a2-a94c-49cd-8e0f-04a54a59dda5">
