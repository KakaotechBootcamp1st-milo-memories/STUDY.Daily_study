# React 기본과 상태관리

## React

UI를 개발하기 위한 컴포넌트 기반 아키텍쳐를 제공하는 JS 라이브러리

### 특징

컴포넌트 기반 : UI를 작은 독립적인 부분으로 나누어 관리 가능

단방향 데이터 흐름

재사용 가능한 컴포넌트

가상 DOM : 실제 DOM과 동기화되어 UI 변경 시 빠른 업데이트 가능

### 가상 DOM 개념과 장점

React는 상태가 업데이트될 떄마다 가상 DOM과 실제 DOM을 비교하여 실제 DOM에 필요한 최소한의 변경만을 반영하여 랜더링하므로 성능이 향상

가상 DOM을 통해 효율적인 업데이트를 가능하게 하여 빠른 랜더링과 최적화된 성능을 제공하고 특정 기능에 종속되지 않아 여러 환경에서 일관된 동작을 보장한다.

## 주요 React 라이브러리 및 도구 소개

- Create React APP(CRA) : React 앱을 빠르게 시작할 수 있는 공식 CLI 도구
- React Router : React 앱의 라우팅을 관리, SPA에서 페이지 간 이동을 쉽게 구현 가능
- Redux : 앱의 상태 관리를 위한 라이브러리, 복잡한 상태 관리 로직을 간결하게 유지 가능
- React Query : 서버 상태를 관리하고 데이터 패칭을 간소화하는 라이브러리, 캐싱, 동기화, 서버 상태 관리 등을 효율적으로 관리
- Styled-components : 컴포넌트 기반 스타일링 도구, JS 코드 내에서 CSS를 작성하여 관리
- Tailwind CSS : 미리 정의된 CSS 클래스를 사용하여 개별 스타일링할 수 있는 도구, 커스터마이징과 재사용성에 강점
- NextUI : 최신 UI 컴포넌트 라이브러리, 다크 모드, 테마 커스터마이징 등의 기능

## 컴포넌트

UI를 구성하는 독립적인 단위(블록)이며 재사용 가능한 코드 블록

각 컴포넌트는 자신만의 상태와 UI를 가지며 다른 컴포넌트와 독립적으로 작동

React에서는 하나의 파일에서 하나의 컴포넌트를 구성하는 것이 일반적

### 종류

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/0d7b76f5-1eaf-4779-b1fe-0961f688d6b2)

- 함수형 컴포넌트
    - JS 함수로 function키워드 혹은 화살표 함수를 통해 구현
    - 상태관리와 생명주기 메소드를 사용하기 위해 React Hooks를 사용 가능 → 유연성이 높음
    - 코드가 간결하기 이해하기 쉬우며 클래스형 컴포넌트보다 메모리 사용량이 적다.
    
    ![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/e55134bc-52d6-4ff1-9725-c235d2306444)
    
    - 별도의 클래스를 선언할 필요 없이 함수 형태로 UI를 정의할 수 있음
- 클래스형 컴포넌트
    - ES6클래스를 사용하여 작성
    - React Component를 상속받아 생성되며 상태와 생명주기 메소드 포함
    - React Hooks의 도입으로 함수형 컴포넌트로 대체되는 추세
    - 별도의 상태 관리를 위한 메소드를 클래스 내에서 정의하고 사용 가능
    - 생명주기 메소드를 통해 컴포넌트의 마운트, 업데이트 등 관리 가능

## JSX란

- JSX는 JS와 XML을 결합한 확장 문법으로 UI를 표현하기 위해 사용
- JS 코드 내에 HTML과 비슷한 문법을 사용하여 React 요소를 생성할 수 있게 해줌
- JSX는 React.createElement()함수 호출로 변환되어 React와 브라우저가 이해할 수 있는 JS 객체로 변환됨
- HTML과 비슷하지만 미세한 차이가 있음

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/b2c56893-7d02-496a-bf3c-6b3ecd3c0e1e)

### 장점

읽기 쉬운 코드

익숙한 HTML 문법 사용

컴포넌트 구조 명확화 : 컴포넌트 구조가 명확히 드러나며 각 요소가 이벤트 핸들러에 어떻게 결합되어있는지 쉽게 파악 가능

### 특징

중괄호를 사용한 JS 코드 삽입

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/33675b81-38ae-42b7-a712-e67e624ac5f3)


모든 태그는 닫혀있어야하고 단일 태그는 self-closing태그로 작성

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/e551e6c5-6ec5-4b05-8848-39a2a95300d4)

### Key

리스트를 렌더링할 때 각 항목에 고유한 식별자 부여

리스트 항목 간 식별을 통해 어떤 항목이 변경, 추가, 삭제되었는지 알 수 있고 이를 통해 재렌더링 성능 최적화 가능

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/a0529800-3267-4d42-8c5a-f8502e7d0415)


### React Hooks

함수형 컴포넌트에서도 상태 관리와 다양한 리액트 기능을 사용하기 위한 문법

일반적으로 함수 이름 앞에는 use가 사용됨

클래스 컴포넌트보다 간결하고 가동성이 좋으며 상태 관리나 부수 효과 로직을 별도의 훅으로 분리하여 재사용 용이

테스트가 쉬워지며 테스트 코드가 간단해짐

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/bb944c46-ec70-4ec6-a9d9-91067f4d44c9)


다양한 라이브러리로 로직을 빠르게 작성 가능

- React Hook Form
- React Use
- useHooks

# 상태와 속성

## 상태

상태는 컴포넌트 내에서 관리되는 데이터로 각각의 컴포넌트는 자체적인 상태를 가질 수 있으며 컴포넌트 생명주기동안 변경될 수 있다.

함수형 컴포넌트에서는 useState 훅을 통해, 클래스형 컴포넌트에서는 클래스의 state 속성을 통해 관리

상태는 UI의 동적인 변화를 표ㅗ현하고 사용자 상호작용에 따라 데이터를 저장하고 업데이트하는 데 사용

클래스형 컴포넌트에서는 setState로 상태 업데이트

상태가 변경될 때마다 컴포넌트가 자동으로 리렌더링되어 UI가 업데이트됨

## 속성

부모 컴포넌트에서 자식 컴포넌트로 데이터를 전달할 때 사용되며 컴포넌트 내부에서 읽기 전용으로 사용되며 변경할 수 없다.

컴포넌트 간 데이터 전달을 통해 재사용성을 높이고 구조를 모듈화하여 관리할 수 있다.

동적으로 데이터를 전달하므로 다양한 상황에서 유연하게 대응 가능

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/e9e9457a-333e-490a-9202-0b825c257709)


- children 속성
    - 리액트에서는 컴포넌트의 태그 사이에 위치한 요소들이 children props로 전달됨
    - 부모 컴포넌트에서 자식 요소들을 포함하고 조작할 수 있음
- 함수형 children
    - JSX에서 중괄호를 통해 JS 코드를 넣는 방식으로 Children을 함수형으로 설정하여 전달 가능

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/ef55f072-d096-4349-b3be-a5d04d1742e4)


# 이벤트 처리

React에서는 DOM 요소에 이벤트를 처리하는 방식이 일반적인 HTML과 다름

JS의 이벤트핸들러와 유사하지만 몇가지 차이가 있음

React 이벤트에서는 소문자 대신 camelCase를 사용(HTML : onclick vs React : onClick)

## 이벤트 처리 방법

- 이벤트 핸들러 등록
    - DOM 요소에 직접 등록, onClick, onChacnge, onSubmit
- 이벤트 핸들러 구현 : 함수 형태의 이벤트 핸들러를 정의하고 이벤트 속성에 할당
- 이벤트 객체
    - React 이벤트 핸들러는 항상 첫 번째 인수로 이벤트 객체를 받음
    - DOM 이벤트와 같은 방식으로 동작하지만 React에서는 크로스 브라우징을 처리하기 위해 일관된 API 제공
    - 이벤트에 대한 추가 정보를 얻거나

## 주요 이벤트 종류

- onClick : 버튼이나 다른 요소를 클릭할 때 발생하는 이벤트
- onSubmit
- onChange
- onMouseOver…
- onKeyDown…

# 리액트 생명 주기

리액트 컴포넌트는 여러 단계를 거쳐 생성, 업데이트, 소멸됨

이런 과정에서 특정 시점에 실행되는 메소드들이 있는데 이를 통해 컴포넌트 상태와 동작을 관리 가능

생명 주기 메소드는 클래스형 컴포넌트에서만 사용가능하며 함수형 컴포넌트에서는 useEffect훅을 사용하여 유사한 동작 수행 가능

useEffect 혹은 컴포넌트 랜더링 때마다 특정 적업을 수행하도록 설정할 수 있으며 마운팅, 업데이트, 언마운팅 단계에서 필요한 동작 지정 가능

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/b684b882-c18a-41bc-81e9-46e979867197)


## 주요 생명 주기

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/a9d1f9cb-7823-4788-a11d-5cc31c315b96)


- 마운팅 : 컴포넌트 생성 시 초기 상태 설정, 컴포넌트가 화면에 나타날 때 초기 데이터 로드나 외부 API 호출 수행 가능
- 업데이트 : 컴포넌트 상태가 변경될 때 마다 UI 업데이트 가능, 성능 최적화를 위해 업데이트를 처리할지 여부 결정 가능
- 언마운팅 : 컴포넌트가 제거되기 전 정리 작업 수행 가능

# useState와 useReducer를 이용한 상태 관리

## useState

함수형 컴포넌트에서 상태를 관리하기 위한 훅

상태 변수와 해당 상태를 갱신할 수 있는 함수를 제공받아 사용

간단하고 직관적으로 상태 관리가 가능하며 여러 개의 상태를 독립적으로 관리 가능

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/f82030b7-5d2a-447e-bb07-bd35d433c6df)


## useReducer

함수형 컴포넌트에서 복잡한 상태 관리 로직을 처리하기 위한 훅으로 상태를 업데이트하는 로직을 더 세밀하게 제어 가능

현재 상태와 상태를 업데이트하는 액션, 액션을 처리하는 리듀서 함수를 받아 사용

복잡한 상태 관리 로직을 구현할 때 유용하며 다양한 액션에 따라 상태 변경 가능

### useReduce의 Flux 패턴

- 액션 : 상태 변경의 이벤트를 설명하는 객체
- 디스패처 : 액션을 리듀서로 전달
- 리듀서 : 현재 상태와 액션을 받아 새로운 상태를 반환

### 사용하는 이유

- 복잡한 상태 관리
    - useState는 단순한 상태 값만 관리할 수 있지만 useReducer는 복잡한 상태 로직을 다루기에 적합함
    - 상태와 그 상태를 업데이트하는 로직을 하나의 리듀서 함수로 관리 가능
    - 앱 규모가 크거나 상태 관리가 복잡할 때 유용
- 컴포넌트 로직 분리
    - 상태와 업데이트 로직을 하나의 단일 객체로 관리하기 때문에 컴포넌트의 UI로직과 분리 가능 → 간결하고 재사용성 증가

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/36459e46-8cbf-4a1b-a333-8b7df8c4a3fa)


- 순수 함수 리듀서
    - 리듀서는 순수 함수로 작성되어야 하며 이전 상태를 변경하지 않고 새로운 상태를 반환해야함
    - 이는 함수 예측 가능성과 테스트 용이성을 높이며 버그를 줄이는데 도움을 줌

> 순수 함수
동일 입력에 대해 항상 동일 결과를 반환
결과 반환 외에는 아무런 일도 하지 않음
함수 실행이 외부 환경에 영향을 미치지 않음
> 

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/4a1521e9-46e8-43f5-b429-1e6798daaa80)


# Context API를 이용한 상태 관리

리액트에서 전역적으로 상태를 관리하기 위한 메커니즘

모든 컴포넌트 혹은 개발자가 설정한 범위 내의 컴포넌트에서 상태를 공유할 수 있음

## 필요한 이유

1. 복잡한 컴포넌트 계층 구조에서의 상태 전파
- 리액트에서는 props를 통해 상위에서 하위로 데이터를 전달하는데 컴포넌트 계층 구조가 깊어질수록 데이터 전달이 번거로워짐(Prop drilling 문제)
- 전역 상태 관리는 중첩된 컴포넌트 구조에서 상태를 일관되게 유지하고 필요한 곳에서 쉽게 접근할 수 있도록 도와줌
1. 상태 공유와 재사용성 증대
- 사용자 인증 상태, 테마 등 여러 컴포넌트가 동일한 상태를 공유해야하는 경우 전역 상태를 사용하면 이런 데이터를 각 컴포넌트마다 props로 전달하지 않고 필요한 곳에서 직접 접근할 수 있어 코드 중복을 줄이고 재사용성 증대 가능
1. 상태 관리의 중앙 집중화
- 전역 상태 관리는 앱 내에서 상태를 중앙 집중화하여 관리 가능

## 사용 예제

### Context 객체 생성

- React.createContext() 함수로 Context 객체 생성
- Provider, Consumer를 활용하여 전역 상태를 선언하고 관리 가능

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/47842e66-541e-4afe-a18b-8e5d1a061bd1)


### Provider 컴포넌트

- 상위 컴포넌트에서 Provider 컴포넌트를 사용하여 전역 상태를 정의하고 제공하는 역할
- Provider 컴포넌트의 하위 컴포넌트들이 Context가 제공하는

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/65483e01-34c5-4dc8-a26e-878222c2037f)


### Consumer 컴포넌트

Context에서  제공하는 상태에 접근

함수형 컴포넌트에서는 useContext 훅을 사용하여 상태를 간편하게 받아올 수 있음(권장)

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/699d4288-da3d-4545-92a9-3216c1a43e0b)


클래스형 컴포넌트에서는 Context의 Consumer 컴포넌트를 사용하여 상태를 간편하게 받아올 수 있음

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/3aab3663-1157-46f8-87c0-81db9a85383c)

혹은 Class.contextType을 사용하면 더 간단하게 전역 상태를 받아올 수 있음(권장)

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/2cb6ab69-3d84-4547-863f-ae59c79ea4f5)

## Context API 사용 시 고려 사항

- 복잡성 증가
    - 앱의 전역 상태가 많은 컴포넌트에 걸쳐 퍼져서 상태의 흐름을 이해하기 어렵고 코드 복잡성이 증가할 수 있다.
- 성능 문제
    - Context를 사용할 떄 모든 Consumer는 Provider가 업데이트될 때마다 다시 렌더링 되므로 Provider가 자주 업데이트되는 경우 성능 문제 발생 가능

## 다양한 전역 상태 관리 라이브러리

- Redux : 가장 널리 사용되는 상태 관리 라이브러리로 복잡한 앱 상태 관리에 적합. Flux 아키텍쳐 기반이며 예측 가능한 상태 변경과 미들 웨어를 통한 확장성이 큰 장점
- MobX : 상태 관리와 관련된 반응형 프로그래밍 패러다임을 지원하는 라이브러리로 Observables와 함께 사용하여 상태 변경을 감지하고 자동으로 UI 업데이트 가능
- Recoil : 페이스북에서 개발한 상태 관리 라이브러리로 React의 복잡한 상태를 관리하기 위해 설계됨, 상태의 원자성을 중심으로 한 다양한 고급 기능 제공
- Zustand : 간단하고 직관적인 상태 관리를 위한 라이브러리, 컴포넌트 내 간편하게 사용할 수 있는 API와 함께 상태를 관리하며 컨텍스트 API보다 더 단순하고 성능이 우수
