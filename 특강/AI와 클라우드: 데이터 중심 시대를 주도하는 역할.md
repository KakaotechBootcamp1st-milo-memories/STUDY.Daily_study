카카오 클라우드 엔지니어가 들려주는 취업 준비 방법

# 취업을 위해 뭘해야 하나요??
- 할 수 있는 일들은 다양하고 요구사항도 제각각이다.
- 지원하고 싶은 곳에서 요구하는 부분이 어떤 것이 있는지 찾아보자.
- 무작정 다 공부하는 것보다는 선택과 집중!

# Programming Language
- 너무 비주류만 아니라면 사실 어떤 언어든 큰 상관
  - 다만 널리 사용될수록 지원 가능한 곳이 더 많다.
- 한 언어를 깊게 사용하다보면 다른 언어도 금방 할 수 있다.
- 회사에서는 개발 Ground Rule을 정해서 하기 때문에 내 의지와 상관없는 경우가 많다.
- 희망하는 포지션에서 주로 사용하는 언어를 선택하는게 제일 유리하다.
- 지원하고자 하는 회사의 Job Description을 확인하는게 좋음

# 권장 역량
- Backend
  - REST API(with swagger), GraphQL
  - MessageQueue(MQ)
  - Framework 사용 경험
    - java - spring boot, kotlin
    - python - flask, django
    - go - gin, chi
    - node.js - express, nest
## Cloud 개발자 심화 역량
- Docker
  - dockerfile, layer 개념 이해
  - cgroup, namespace 이해
  - multi-stage build
- Kubernetes
  - Kubernetes 동작 원리 이해
  - deplyment, service, ingress 이해
- Linux
  - 기본적인 명령어와 네트워크 이해
## 자소서 작성 팁
1. 간략하게
2. 기술 스펙은 명확하게
3. 프로젝트에서 내가 한 부분을 바로 알 수 있게
- 참고: https://wonny.space/writing/work/engineer-resume

# 코딩테스트 준비
- LeetCode - https://leetcode.com/problemset/all/
- BOJ - https://www.acmicpc.net/workbook/top
- Programmers - https://school.programmers.co.kr/learn/challenges?order=recent

- 코딩테스트는 왕도가 없다. 타겟회사의 문제 스타일을 확인하고 최소 하루 한 문제 풀자
  - 입사에 필요한 코딩테스트는 딱 필요한 수준만 하면 된다. 잘한다고 상주는게 아니다
  - 어려운 문제에 시간을 많이 쓰지말고 수준에 맞는 다양한 문제를 풀자
  - 어떻게 풀어야할지 감조차 안오는 문제는 답지부터보고 풀이를 익히는게 도움이 된다
  - 같이 취준하는 친구들과 스터디를 해서 같이 풀면 수월하다
- 지원한 곳이 Go만 쓴다는데, 코테도 Go로 해야되나요? -> No, Python으로 해도 상관X

# 면접 준비
- 신입 공채 지원자에게 물어볼건 CS 질문 & 코딩 테스트 질문이 거의 전부
  - CS는 꼬리 질문이 많이 들어온다. 예상 질문 -> 예상 답변 -> 예상 질문 -> 예상 답변을 준비하자
- 모르는건 모른다고 해도 괜찮다
  - 괜히 모르는걸 아는 것처럼 말하려다, 스스로 꼬일 수 있다
- 결국 면접관은 같이 일하고 싶은 사람을 찾는 것이다.
  - 대답하기 어려운 내용이 나오면 태도나 자세면서 저 내용을 떠올리면서 답변하자
- 대답은 간결하게, 물어보지도 않은 내용을 안다고 괜히 답변할 필요없다
- 면접 전형이 여러번 있는 경우, 면접관이 앞선 차수 기록을 조회할 수 있으므로 면접이 끝난 뒤 기억나는 대로 기록하고 스스로 피드백한다.
  - 나왔던 질문. 답변 기록 및 대답하지 못한 질문은 필수로 꼭 다시 찾아본다. 다음 모든 면접에서 도움이 된다

- [질문 모음집](https://github.com/DopplerHQ/awesome-interview-questions)
  - 이렇게 질문을 github에 모아놓은 것을 참고해도 된다.
  - 그 중에 본인에게 맞는 것을 선택하여 준비 (기본 CS, 특정 언어 또는 프레임워크..)
- Reverse Interview Question도 준비해서 내가 이 회사에 관심이 많다는걸 어필하자!
  - [Reverse Interview](https://github.com/jaeyeophan/interview_question_for_beginner) : 반대(Reverse)와 면접(Interview)의 합성어로 면접관과 면접자가 역할을 바꿔 진행하는 면접을 의미
 
## 면접 필수 질문 5개
1. 자기소개 1분
   - 지원한 직무 이름 기억하기
2. 강점
   - 두괄식
   - 경험 위주
3. 지원 동기
4. 성격의 장단점
   - mbti를 이용해도 좋음
5. 마지막 할 말

## 면접 에상 기본 문제
- 코딩테스트
  - 라이브 코딩(회사에 따라 다름)
  - (본인코드 보면서) 왜 그렇게 풀었는지?
  - 더 좋은 풀이방법이 있다고 생각하는지?
  - 이 문제는 무슨 알고리즘으로 푸는건지?
- 프로젝트
  - 프로젝트 수행 시 본인은 무슨 역할을 했는지(기술적인 면, 협동적인 면 모두)
  - 왜 특정 기술 스택을 선택하여 썼는지? (예를들면 RDB vs noSQL)
  - 프로젝트 실패/성공 원인이 뭐라고 생각하는지?
  - 본인이 한계 맞는지 검증을 위한 추가 질문

## 면접 예상 심화 질문
- GC (Java, go, python)
- VM vs Container
- cgroup, namespace
- Docker layer
- Docker multi-stage build
- Sidecar pattern

# 개발자로서 추천하고 싶은 것들
- 자기개발
  - 책
  - 스터디
  - 네트워킹
    - 주변 동료들은 언제든 다시 도움이 된다. 잘 챙기자

