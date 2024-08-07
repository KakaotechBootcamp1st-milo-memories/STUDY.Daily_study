# 버전 관리

## 정의

- 파일이나 프로젝트의 변경 사항을 시간에 따라 기록하고 추적하는 시스템
- 특정 시점의 버전을 불러올 수 있고 변경 내역을 확인하고 관리할 수 있음
- 주로 소프트웨어 개발에 사용되지만 문서 작성, 디자인 작업 등 다양한 분야에서도 활용

## 중요성

- 변경 이력 추적: 누가, 언제, 무엇을 변경했는지 정확히 알 수 있음
- 협업 용이성
- 백업과 복구
- 실험적 개발
- 품질 관리

## 역사

- 수동 버전 관리(1950년대~)
- 로컬 버전 관리 시스템(1980년대~)
    - 로컬 컴퓨터에서 변경 사항 관리
    - RCS 등
- 중앙 집중식 버전 관리 시스템(1990년대~)
    - 중앙 서버에서 모든 버전 관리
    - CVS, SVN 등
- 분산 버전 관리 시스템(2000년대~)
    - 모든 개발자가 전체 저장소의 복사본을 가지고 작업
    - Git(2005), Mercurial(2005) 등
- 클라우드 기반 버전 관리(2010년대~)
    - GitHub, GitLab, Bitbucket 등의 플랫폼 등장
    - 버전 관라와 협업 도구 통합

# Git 기본 개념

## 분산형 버전 관리 시스템(DVCS)

- Git
    - 모든 개발자가 전체 프로젝트 히스토리를 로컬에 저장
    - 중앙 서버 없이도 모든 작업을 로컬에서 수행 가능
    - 네트워크가 불안하거나 중앙 서버가 다운되어도 작업 가능
- SVN(SubVersion)
    - 중앙집중식 버전 관리 시스템
    - 모든 데이터는 중앙 서버에 저장되고 작업 내역을 중앙 서버에서 관리
    - 중앙 서버에 의존적이며 서버가 다운되면 작업에 저장

## Git의 기본 요소

- 저장소(Repository)
    - 프로젝트의 모든 파일과 히스토리를 포함하는 저장소
- 커밋(Commit)
    - 파일 변경 사항의 스냅샷
    - 고유한 SHA-1 해시 ID로 식별됨
    - 코드 이력을 구성하는 기본 단위
- 브랜치(Branch)
    - 독립적인 작업 공간을 제공하는 구조
    - 서로 다른 기능이나 버전을 동시에 개발할 수 있도록 함
    - 기본 브랜치는 보통 ‘master’ 또는 ‘main’
- 병합(Merge)
    - 현 브랜치의 변경사항을 다른 브랜치에 통합
    - 서로 다른 브랜치에서 작업한 내용을 통합하여 일관성있는 히스토리 유지
- 원격 저장소(Remote Repository)
    - 인터넷이나 네트워크에 호스팅된 저장소
    - 여러 개발자가 협업할 수 있도록 변경사항 공유 가능
    - GitHub, GitLab, Bitbucket 등이 원격 저장소 서비스 제공
- 푸시(Push)
    - 로컬 저장소의 변경 사항을 원격 저장소에 반영하는 작업
    - 로컬 저장소의 커밋을 원격 저장소 특정 브랜치에 반영
- 풀(Pull)
    - 원격 저장소를 복제하여 로컬에 생성
    - 프로젝트 초기 설정 시 원격 저장소의 모든 파일과 히스토리를 로컬에 복제
- 스테이징 영역(Staging Area)
    - 커밋할 변경사항을 준비하는 중간 영역
    - 커밋하기 전 어떤 변경 사항이 포함될지 설정

<img width="523" alt="image" src="https://github.com/user-attachments/assets/a19c4cf7-3f6e-48f5-a8fe-5466665405c8">

# Git 기본 명령어

## 로컬 저장소 시작하기

```sql
git init
```

- 현재 작업 디렉토리를 GIt 저장소로 변환
- Git이 버전 관리를 할 수 있도록 디렉토리 내에 .git이라는 숨김 디렉토리 생성
- .git 디렉토리는 Git이 필요한 모든 메타데이터와 객체를 저장
- 기본적으로 모든 Git 명령어는 GIt 저장소 디렉토리 아래에서 실행

<img width="523" alt="image" src="https://github.com/user-attachments/assets/7ab1e6a3-5d2c-4e0b-9c3d-30bdfd0f6032">

## 로컬 저장소 상태 확인

```sql
git status
```

- 현재 작업 디렉토리와 스테이징 영역의 상태를 보여줌
- 수정 파일, 추가 파일, 스테이징 영역에 있는 파일 등을 추적하여 현재 작업 상태 확인 가능
- 커밋하기 전 어떤 파일이 수정되었고 어떤 파일이 스테이징되었는지 확인하는데 유용

### 출력 내용

<img width="523" alt="image" src="https://github.com/user-attachments/assets/2669a5e7-25bc-4f02-a619-4b9af34c22eb">

- Untracked files: Git이 현재 관리하지 않는 새 파일 목록
- Changes not staged for commit: 수정된 파일이지만 스테이징 영역에 추가되지 않은 상태
- Changes to be commited: 스테이징 영역에 추가되어 커밋 준비가 완료된 파일

## 파일 변경 사항을 스테이징 영역에 추가

```sql
git add <file or directory>

git add -A #모든 변경 사항 추가
git add . #현재 디렉토리 내 모든 변경 사항 추가
git add index.js # 특정 파일 추가
```

- 스테이징 영역은 커밋할 파일들을 임시로 저장하는 영역
- 작업 디렉토리에서 변경된 파일을 선택적으로 스테이징 영역에 추가하여 원하는 파일만 커밋 가능

## 스테이징 영역의 변경 사항을 커밋하기

```sql
git commit

git commit -m "Commit message"
```

- 스테이징 영역에 추가된 변경 사항을 커밋하여 로컬 저장소의 히스토리에 저장함
- 커밋 메시지는 변경 사항을 설명하는 텍스트
- -m 옵션을 사용하지 않으면 Vim 에디터로 커밋 메시지 작성

## 커밋 메시지 컨벤션

```sql
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

- 타입은 필수로 작성해야하며 범위는 선택 사항
- 설명은 타입/범위 다음에 반드시 작성
- 본문과 푸터는 선택사항
- 주요 변경 사항은 Type/Scope 뒤에 !를 추가하거나 푸터에 BREAKING CHANGE를 명시

```bash
[Without Scope]
feat: allow provided config object to extend other configs

[With Scope]
feat(lang): add Polish language

[BREAKING CHANGE "!"]
feat(api)!: send an email to the customer when a product is shipped

[BREAKING CHANGE footer]
feat: allow provided config object to extend other configs

BREAKING CHANGE: `extends` key in config file is now used

[Full Commit Message]
fix: prevent racing of requests

Introduce a request id and a reference to latest request. Dismiss incoming responses other than from latest request.

Remove timeouts which were used to mitigate the racing issue but are obsolete now.

Reviewed-by: Z
Refs: #123
```

| 타입 이름 | 설명 |
| --- | --- |
| feat | 새로운 기능을 추가합니다. |
| fix | 버그를 수정합니다. |
| style | 코드 포맷 변경, 세미콜론 누락 등 코드 수정이 없는 경우에 사용합니다. |
| refactor | 프로덕션 코드를 리팩토링합니다. |
| comment | 필요한 주석을 추가하거나 변경합니다. |
| docs | 문서 작업을 수정합니다. |
| test | 테스트 코드 추가나 리팩토링을 포함하며, 프로덕션 코드는 변경되지 않습니다. |
| perf | 성능 개선 작업을 수행합니다. |
| build | 빌드 관련 작업을 수행합니다. |
| chore | 그 외 자잘한 수정에 대한 커밋을 말합니다. 주로 코드에는 변경 사항이 없는 경우입니다. |

# 브랜치와 병합

## 브랜치 생성

```bash
git branch <branch-name>

git branch kakao-login
```

- 기능 개발, 버그 수정 등을 독립적으로 진행할 수 있도록 별도의 새로운 브랜치 생성

## 브랜치 전환

```bash
git checkout <branch-name>

git checkout kakao-login
git checkout main
```

- 현재 브랜치를 지정한 브랜치로 전환
- 작업할 브랜치를 선택하여 해당 브랜치에서 커밋 진행 가능

## 브랜치 생성과 동시에 전환

```bash
git checkout -b <branch-name>

git checkout -b google-login
```

## 브랜치 병합

```bash
git merge <branch-name>

git merge google-login
```

- 다른 브랜치에서 작업한 내용을 현재 브랜치에 병합
- 즉, 현재 브랜치가 main이라면 main 브랜치로 google-login 브랜치의 변경 사항을 가져와 병합함

### 병합 충돌(Conflict)

- 브랜치를 병합할 때 동일한 파일의 동일 부분에서 서로 다른 변경 사항이 있을 경우 충돌 발생
- 컴퓨터는 어떤 변경 사항이 적용되어야하는지 알 수 없으므로 개발자가 직접 어떤 변경 사항이 적용되어야하는지 선택해야함

### 병합 충돌 해결하기

<img width="523" alt="image" src="https://github.com/user-attachments/assets/7088016e-49cd-442b-81d2-20524794a9d7">

1. 충돌 상태 확인: 충돌이 발생한 파일 목록 확인

```bash
git status
```

1. 충돌 파일 수동 수정
- `<<<<<<< HEAD`: 현재 브랜치의 변경 사항
- `=======`: 변경 사항의 구분
- `>>>>>>> <branch-name>`: 병합하려는 브랜치 변경 사항
1. 충돌 해결 후 파일 추가: 수정한 파일을 스테이징 영역에 추가

```bash
git add conflicted-file.java
```

1. 병합하기: 병합을 완료함. 커밋 메시지는 자동 생성되며 수정 가능

```bash
git commit
```

1. 커밋 상태 확인: 병합 결과와 커밋 로그 확인

```bash
git log --oneline
```

- 충돌 해결 시 주의 사항
    - 충돌 해결 후 작업 내용을 충분히 검토하고 모든 변경 사항이 의도대로 반영되었는지 확인함
    - 병합 . 후테스트를 진행하여 코드가 예상대로 작동하는지 확인

# 원격 저장소

## 원격 저장소와 로컬 저장소 연동

```bash
git remote add origin <url>
```

- 로컬 저장소에 원격 저장소를 연결하여 원격 저장소와 데이터를 주고받을 수 있음

## 원격 저장소 연결 확인하기

```bash
git remote -v
```

- 설정된 원격 저장소의 주소와 설정 상태를 확인하여 연결이 제대로 되었는지 확인 가능
- fetch: fetch 작업에 사용되는 URL을 나타냄, git fetch 명령어를 사용하여 원격 저장소에 데이터를 가져올 때 이 URL이 사용됨
- push: push 작업에 사용되는 URL을 나타냄, git push 명령어를 사용하여 변경 사항을 원격 저장소로 업로드할 때 이 URL이 사용됨
- 이를 통해 원격 저장소의 주소와 로컬 저장소와의 연결 상태를 확인할 수 있으며 원격 저장소와의 데이터 전송 경로 이해 가능

## 원격 저장소 URL 변경

```bash
git remote set -url origin <new-url>
```

- 기존 원격 저장소의 URL 변경
- 원격 저장소 주소가 변경된 경우 업데이트할 때 사용

## 원격 저장소에 로컬 저장소 커밋 반영하기(Push 하기)

```bash
git push origin <branch>

git push origin main
```

- 로컬 저장소의 브랜치와 그 브랜치의 커밋 히스토리를 원격 저장소에 업로드
- 커밋된 모든 변경 사항을 원격 저장소에 업로드하여 백업하거나 팀원들과 공유 가능

## 원격 저장소에서 로컬 저장소로 변경 사항 가져오기(Pull 하기)

```bash
git pull origin <branch>

git pull origin main
```

- 원격 저장소의 변경 사항을 로컬 저장소로 가져와 자동 병합

## 원격 저장소 복제하기(Clone)

```bash
git clone <url>
```

- 원격 저장소의 전체 히스토리와 현재 상태를 로컬로 가져와 독립적인 작업 시작 가능
- 원격 저장소 내용이 로컬 저장소에 복사되며 로컬 저장소는 원격 저장소와 연결
- 클론 작업 후 로컬 저장소의 기본 브랜치는 원격 저장소의 기본 브랜치로 설정됨

# 협업 워크플로우

## Fork

- 원본 저장소를 복제하여 개인 저장소를 만드는 과정
- GitHub, GitLab, Bitbucket 등에서 제공하는 기능

### 용도

- 오픈 소스 프로젝트에 기여하거나 개인적인 변경사항 실험에 사용
- 원본 저장소에 영향을 주지 않고 개인 저장소에서 자유롭게 작업 가능

### 특징

- Fork된 저장소는 원본 저장소와는 별도의 독립된 저장소임
- 원본 저장소와의 동기화는 자동으로 이뤄지지 않으며 수동으로 동기화 작업을 해야함
- Fork한 후 원본 저장소에 변경 사항을 제안할 때는 Pull Request를 통해 진행

### 예시

- 오픈 소스 프로젝트에 기여하기 위해 자신의 GitHub 계정으로 프로젝트를 포크하여 작업을 진행

## Pull Request(PR)

- Fork한 저장소나 개별 브랜치에서 작업한 변경 사항을 원본 저장소에 병합해달라고 요청하는 과정
- GitHub, GitLab, Bitbucket 등에서 제공하는 협업 기능
- 다른 사람들이 작업한 코드를 검토하고 리뷰 후 원본 저장소에 병합하여 코드 품질 유지
- 코드 리뷰를 통해 피드백을 받고 협업을 통해 보장된 코드를 병합 가능

### PR 절차

1. 개인 저장소에서 변경 사항을 커밋하고 푸시
2. 원본 저장소 GitHub 페이지에서 New PullRequest 버튼 클릭
3. 변경 사항을 설명하는 내용 작성
4. 원본 저장소의 유지보수자나 팀원이 코드 리뷰 진행
5. 리뷰 후 변경 사항이 승인되면 원본 저장소에 병합

### 유의 사항

- 코드 품질
    - 코드 스타일: 프로젝트 코드 스타일을 따라야 함
    - 테스트: 모든 관련 테스트를 수행하고 결과 설명
    - 문서화
- 제목과 설명
    - 제목: 변경 사항을 간결하고 명확하게 작성
    - 설명: 변경 사항, 관련 이슈, 기능 요구 사항 등을 자세히 설명
- 리뷰 요청
    - 리뷰어 지정: 적절한 리뷰어를 지정
    - 피드백 반영: 리뷰어의 피드백을 반영하여 PR 업데이트
- 추가 정보
    - 관련 문서: 관련 문서나 링크 포함
    - 체크리스트: PR 제출 전 코드 스타일, 테스트 통과, 문서화 . 등확인

### GitHub PR Templete todtjd

1. PR 템플릿 파일 생성
- GitHub 저장소의 .github 폴더에 PULL_REQUEST_TEMPLETE.md 파일 생성
1. PR 템플릿 작성
- 템플릿 파일에 PR 작성 시 포함해야할 내용과 지침을 마크다운으로 작성

```bash
## 변경 사항

- 변경 사항 설명
- 관련된 이슈 번호 (예: #123)

## 검토 항목

- [ ] 코드 스타일
- [ ] 기능 동작 확인
- [ ] 테스트 수행 여부

## 추가 정보

- 스크린샷 또는 로그 (있다면)
```

1. 커밋 및 푸시
- 작성한 PR 템플릿 파일을 커밋하고 원격 저장소에 푸시
- 여러 템플릿을 만들어 사용 가능

## Git 워크플로우

- 복잡한 프로젝트를 관리하기 위한 Git 브랜치 모델

### 주요 브랜치

- main: 안정화된 코드, 배포 준비 완료 상태
- develop: 개발 중인 최신 코드, 기능 통합
- feature: 새로운 기능 개발, develop에서 분기
- release: 배포 준비, develop에서 분기하여 버그 수정 및 최종 테스트
- hotfix: 긴급 버그 수정, main에서 분기하여 바로 배포

### GitLab Flow

- 단순한 브랜칭 모델, 주로 소규모 팀에서 사용
- main 브랜치에서 작업, 기능 개발 후 PR로 코드 리뷰 후 병합하는 과정을 거침
- GitHub Flow의 변형으로 개발, 배포, 버그 수정 브랜치를 포함
- feature 브랜치의 production 브랜치를 주로 사용하여 지속적 배포 지원

# 고급 Git 사용법

## Rebase

```bash
git checkout kakao-login
git rebase main
```

- rebase는 현재 브랜치의 변경 사항을 지정한 다른 브랜치 위에 재적용하는 방법
- Git에서 브랜치를 통합할 때 사용하는 두 가지 주요 방법 중 하나

### Rebase와 Merge의 차이점

- Merge
    - 두 브랜치의 마지막 커밋을 기준으로 새로운 커밋을 생성하여 통합, 커밋 히스토리가 복잡해질 수 있음
- Rebase
    - 변경 사항을 다른 브랜치의 최신 커밋 위로 재적용하여 히스토리를 깔끔하게 유지함
    - 최종 결과물은 Merge와 동일하지만 히스토리가 선형으로 변함

### Rebase의 장점

- 히스토리 정리
    - 브랜치를 선형으로 만들어 커밋 히스토리가 깔끔하고 이해가 쉬워짐
- 작업 순서 유지
    - 병렬 작업 후에도 모든 작업이 순차적으로 진행된 것처럼 보임

### Rebase 사용 시 유의 사항

- 공개 저장소에서의 Rebase 금지
    - 공개된 브랜치에서 수행하면 다른 팀원이 의존하는 커밋이 변경되므로 Merge를 사용해야함
- Rebase의 위험성
    - Rebase로 인해 동일한 내용의 커밋이 두 번 생성될 . 수있으며 이로 인해 히스토리가 혼란스러워질 수 있음
    - 이미 Push한 커밋에 대해 Rebase를 수행하는 것은 피해야 함

## Cherry-pick

```bash
git cherry-pick <commit-hash>
```

- 지정한 커밋을 현재 브랜치에 적용
- 필요없는 모든 커밋을 포함하지 않고 특정 커밋만을 선택적으로 가져오고 싶을 때 사용할 수 있음
- 커밋 충돌이 발생할 수 있으며 충돌 해결 후 `git cherry-pick — continue` 명령으롤 입력해 과정을 계속 진행해야함

## Stash

```bash
git stash                       # 현재 변경 사항을 저장
git stash save NAME             # 특정 이름으로 저장
git stash apply                 # 가장 최근 stash 가져오기
git stash pop                   # 가장 최근 stash 가져오고 임시 저장 삭제
git stash apply stash@{n}       # n번째 stash 가져오기
git stash drop stash@{n}        # n번째 stash 삭제
git stash clear                 # 모든 stash 삭제
git stash list                  # stash 목록 보기
```

- 현재 작업 중인 변경 사항을 임시로 저장하고 깨끗한 작업 상태로 되돌림
- 작업 . 중변경 사항을 일시적으로 보관하고 다음 작업을 시작할 때 사용함
- stash 항목은 제거된 후 복원할 수 없으므로 필요할 때는 꼭 복원해야 함

## Reset

```bash
커밋을 되돌리되, 변경 사항은 staging area에 유지합니다.
git reset --soft <commit>

커밋과 staging area를 되돌리지만 작업 디렉토리는 유지합니다.
git reset --mixed <commit>

커밋, staging area, 작업 디렉토리 모두 되돌립니다.
git reset --hard <commit>

가장 최근 커밋을 제거하고 작업 디렉토리도 초기화
git reset --hard HEAD~1
```

- 브랜치 상태를 특정 커밋으로 되돌림
- 실수로 커밋한 변경 사항을 되돌리거나 작업을 초기 상태로 복원할 때 사용
- `—hard` 옵션을 사용할 경우 변경 사항이 모두 사라지므로 신중히 사용해야 함.
