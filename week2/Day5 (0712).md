# 리액트 고급 기능
## 컴포넌트 최적화: Memoization 이해하기

- React에서 컴포넌트가 리랜더링이 되는 조건
    - 컴포넌트의 State가 변경되었을 때
    - 컴포넌트의 props가 변경되었을 때
- React에서의 메모이제이션
    - React는 불필요한 리렌더링을 방지하고 성능을 최적화하기 위해 여러 메모이제이션 기법을 제공
    - 주로 사용되는 메모이제이션 도구는 React.memo,  useMemo, useCallback

## 컴포넌트 최적화: React.memo

React.memo는 고차 컴포넌트(Higher Order Component)로 컴포넌트의 props가 변경되지 않았을 때 리렌더링을 방지

React.memo는 props의 얕은 비교를 수행

props가 복잡한 객체를 가지고 있을 경우, 커스텀 비교 함수를 제공

```jsx
const MyComponent = ({name}) => <div>(name)</div>;

const areEqual = (prevProps, nextProps) =>{
	//true를 반환하면 리렌더링을 하지 않고 false를 반환하면 리렌더링을 함
};

const MyComponent = React.memo(MyComponent, areEqual);
```

## 컴포넌트 최적화 : useMemo

이 Hook은 계산 비용이 높은 함수의 결과값을 메모이제이션하여 불필요한 재계산을 방지해 렌더링 성능을 최적화

의존성 배열의 값이 변경될 때만 재계산

주로 복잡한 계산을 하거나 큰 데이터를 처리하는 함수에 사용함

## 컴포넌트 최적화: useCallback

이 Hook은 함수 자체를 메모이제이션하여 자식 컴포넌트의 불필요한 리렌더링을 방지해 렌더링 성농을 최적화

의존성 배열의 값이 변경될 때만 재계산

주로 자식 컴포넌트에 전달되는 콜백 함수에 사용

## 컴포넌트 최적화 주의사항

- 과도한 사용 피하기 : 모든 값이나 함수를 메모이제이션할 필요가 없고 실제 성능 향상이 필요한 경우에만 사용하는 것이 좋음
- 의존성 배열 관리 : 필요한 모든 값을 의존성 배열에 포함해야 함, 불필요한 값이 포함되지 않도록 주의
- 얕은 비교 이해 : React는 의존성 배열에 대해 얕은 비교를 수행함. 즉, 객체의 참조가 바뀌면 값이 바뀐 것으로 판단. 따라서 객체나 배열의 참조가 변경되면 메모이제이션이 우효화됨
- 성능 측정 : React Devtools의 Profiler를 활용하여 실제 성능이 향상됐는지 확인

## 얕은 비교

useMemo나 useCallback은 의존성 배열의 각 항목에 대해 얕은 비교 수행(객체나 배열의 경우 참조 동등성만을 확인)

→ 객체나 배열의 내용이 같더라도 새로운 참조가 생성되면 React는 이를 변경된 것으로 간주하고 메모이제이션된 값이나 함수를 재생성함

```jsx
const obj = {id:1};
const memoizedValue = useMemo(() => expensive(obj), [obj]);
```

이 경우 obj의 내용이 변경되지 않아도 컴포넌트가 리렌더링될 때마다 새로운 객체 참조가 생성되어 memoizedValue가 재계산됨

이를 방지하기 위한 방법

- 객체나 배열 대신 원시 값을 의존성으로 사용
- 객체나 배열을 컴포넌트 외부에서 생성하거나 useMemo를 사용하여 메모이제이션
- 필요한 경우 커스텀 비교 함수를 사용하는 방법을 고려

## 코드 분할과 지연 로딩

- 코드 분할은 앱의 한 페이지를 더 작은 조각(청크)으로 나누고 필요한 시점에 로드하는 기술
- 이 기술은 초기 로딩 시간을 줄이고 전체적인 앱 성능을 향상시키는데 중요
- React에서는 React.lazy()와 Suspense를 통해 코드 분할과 지연 로딩 구현 가능
- 실제 성능 향상을 측정하고 사용자 경험을 고려하여 적절히 적용하는 것이 중요

## React.lazy()를 활용한 동적 임포트

React.lazy()는 동적으로 컴포넌트를 임포트할 수 있게 해주는 함수

컴포넌트가 실제로 렌더링되어야할 때 로드되도록 할 수 있음

동적 임포트를 활용하면 웹 페이지의 포기 로딩 시간을 크게 줄이고 필요한 컴포넌트만 그때그때 로드하여 전체적인 성능 개선 가능

React.lazy로 로드되는 컴포넌트는 반드시 default export를 사용해야함

```jsx
const HomePage = React.lazy(() => import("./HomePage"));
const ProfilePage = React.lazy(() => import("./ProfilePage"));
const SettingPage = React.lazy(() => import("./SettingPage"));

const App = () => (
	<Router>
		<Switch>
			<Route exact path = "/" component={HomePage}/>
			<Route path = "/profile" component={ProfilePage}/>
			<Route path = "/settings" component={SettingPage}/>
		</Switch>
	</Router>
);
```

## Suspense로 로딩 처리하기

Suspense는 아직 렌더링이 준비되지 않은 컴포넌트가 있을 때 렌더링할 컴포넌트를 설정할 수 있게 해주는 컴포넌트

React.lazy()와 함께 사용되어 동적으로 로드되는 컴포넌트의 로딩 상태를 처리 가능

```jsx
<Suspense fallback={<div>Loading...</div>}>
	<OtherCompoonent2 /> //React.lazy()로 래핑된 컴포넌트
	<OtherCompoonent2 /> //여러 컴포넌트를 처리할 수 있음.
	<Suspense fallback={<div>Loding2...</div>}>
		<OtherComponent3/> // Suspense를 중첩으로 사용할 수 있음
	</Suspense>
</Suspense>
```

## Error Boundaries

컴포넌트 트리의 하위에서 발생하는 자바스크립트 에러를 캐리하고 에러 발생 시 풀백 UI를 표시하며 전체 앱이 완전히 중단되는 것을 방지함

구현 방법 : Error Boundary는 다음 생명주기 메소드 중 하나 이상을 정의한 클래스 컴포넌트

- static getDerivedStateFromError()
- componentDidCatch

특징

- Error Boundaries는 트리 내에서 깊숙이 중첩된 에러도 캐치
- 여러 Error Boundaries를 중첩하여 사용할 수 있어 세분화된 에러 처리 가능
- 클래스 컴포넌트로 구현하지만 함수형 컴포넌트에서도 Error Boundary 사용 가능

제한 사항

- 다음과 같은 에러는 캐치하지 않음
    - 이벤트 핸들러 내부의 에러
    - 비동기 코드(예: setTimeout이나 requestAnimationFrame 콜백)
    - 서버 사이드 렌더링
    - Error Boundary 자체에서 발생하는 에러

<img width="528" alt="image" src="https://github.com/user-attachments/assets/e95ac0ef-bbff-4379-9c85-111aade2c19b">

## Error Boundaries

Suspense와 함께 사용하여 비동기 컴포넌트를 불러오지 못했을 때 에러 캐치 가능

```jsx
<ErrorBoundary>
	<Suspense fallback={<Loading/>}>
		<LazyComponent/>
	</Suspense>
</ErrorBoundary>
```

컴포넌트가 로딩되는 동안 `Loading…` 메시지가 표시됨

컴포넌트 로딩이 성공하면 정상적으로 렌더링됨

로딩 중 또는 렌더링 중 에러가 발생하면 Error Boundary가 이를 캐치하고 에러 메시지를 표시

# 라우팅과 네비게이션

## Single Page Application(SPA)

SPA(Single Page Application)는 하나의 HTML 페이지로 구성된 웹 앱을 말하며 필요한 컨텐츠를 동적으로 변경하여 사용자에게 제공

특징

- 초기 로딩 후 페이지 전체를 다시 로드하지 않음
- 자바스크립트를 사용하여 동적으로 컨텐츠를 변경
- URL에 따라 적절한 컴포넌트를 렌더링
- 빠른 사용자 경험 제공
- 서버 부하 감소

<img width="528" alt="image" src="https://github.com/user-attachments/assets/82ef10fd-969c-4618-82e6-bc4008e0e868">

## React Router

React 앱에서 라우팅은 사용자가 다양한 페이지를 탐색할 수 있게 해주는 중요한 기능, React Router는 이를 위한 가장 인기 있는 라이브러리

```jsx
import {BrowserRouter, Routes, Route} from "react-router-dom";

function App(){
	return (
		<BrowserRouter>
			<Routes>
				<Route path="/" element={<Home/>}/>
				<Route path="/about" element={<About/>}/>
				<Route path="/users/:id" element={<User/>}/>
			</Routes>
		</BrowserRouter>
	);
}
```

## React Router의 종류

1. Browser Router
- HTML5 History API 사용
- 깔끔한 URL 제공
- 서버 설정이 필요할 수 있음
- 대부분의 현대적인 웹 애플리케이션에 권장됨
1. HashRouter
- URL의 해시 부분을 사용 (예: /#/users/123)
- 서버 설정이 필요없어 정적 파일 호스팅에 적합
    - 브라우저는 URL에서 해시(#) 이후의 부분을 서버로 전송하지 않음
    - 서버는 항상 해시 이전의 기본 URL만 받게 됨
- 검색 엔진이 해시 이후의 콘텐츠를 인식하지 못할 수 있어 SEO에 불리할 수 있음
1. MemoryRouter
- 앱 메모리에 히스토리가 저장되어 URL이 변경되지 않음
- 내부적으로 자바스크립트 배열을 사용하여 히스토리를 관리
- 테스팅이나 비브라우저 환경(React Native 등)에 유용

## 동적 라우팅

- :id와 같은 URL 파라미터를 사용하여 동적 라우트를 설정하고 useParams 훅을 통해 이 파라미터에 접근 가능

<img width="528" alt="image" src="https://github.com/user-attachments/assets/1a6903ac-d65b-46c5-a8bb-884c871d84bd">

## 동적 라우팅 내 선택적 파라미터

- 특정 파라미터를 선택적으로 만드려면 괄호() 사용 가능

<img width="528" alt="image" src="https://github.com/user-attachments/assets/5fe3bdb5-4f3a-4d50-9254-3d74b05058e5">

## 컴포넌트를 통해 페이지 이동

React Router에서 제공하는 Link 컴포넌트로 네비게이션 기능을 구현

Link는 내부적으로 <a> 태그로 렌더링되지만 클릭 이벤트를 가로채어 페이지 새로고침을 방지

<img width="528" alt="image" src="https://github.com/user-attachments/assets/60f92e5f-7a51-4d3c-b389-c1b080c02717">

## 프로그래매틱 페이지 이동하기

React Router에서 제공하는 useNavigate 훅으로 프로그래밍 방식으로 네비게이션 구현 가능

<img width="528" alt="image" src="https://github.com/user-attachments/assets/cfd40d18-fd26-4b1f-8c0c-812c9b2b04c4">

## 중첩 라우팅

중첩 라우팅은 부모 라우트 내에 자식 라우트를 정의하는 것

이 때, Outlet 컴포넌트는 부모 라우트 컴포넌트에서 자식 라우트 컴포넌트가 렌더링될 위치를 지정

<img width="528" alt="image" src="https://github.com/user-attachments/assets/0299b315-f321-43d5-a1c3-2381f115ff79">

# 클라이언트 사이드 렌더링(CSR)과 서버 사이드 렌더링(SSR)

## CSR vs SSR

- SSR
    - 서버에서 HTML을 생성하여 클라이언트에 전송
    - 초기 로딩 속도가 빠름
    - SEO에 유리
    - 서버 부하가 증가할 가능성
- CSR
    - 클라이언트에서 자바스크립트로 HTML을 생성
    - 초기 로딩 속도가 느림
    - 사용자 상호 작용에 유리
    - 서버 부하 감소

## CSR 동작 과정

1. 브라우저가 서버에 요청을 보냄
2. 서버는 빈 HTML 파일과 자바스크립트 파일을 응답
3. 브라우저는 HTML 파일을 로드하고 자바스크립트 파일을 다운로드 및 실행
4. 자바스크립트는 필요한 데이터를 API 요청을 통해 가져옴
5. 데이터를 사용하여 DOM을 동적으로 구성하고 최종 UI를 렌더링

## SSR 동작 과정

1. 브라우저가 서버에 요청을 보냄
2. 서버는 요청을 처리하고 필요한 데이터를 가져와 HTML을 생성
3. 생성된 HTML을 클라이언트에 응답
4. 브라우저는 완전한 HTML을 로드하고 초기 렌더링을 완료함
5. 자바스크립트 파일을 다운로드 및 실행하여 상호작용을 활성화

## SSR을 지원하는 프레임워크

- Next.js
- Nuxt.js
- Angular Universal
- Gatsby
- Sapper

## SSR 성능 최적화

- 코드 스플리팅
    - 필요 시점에 필요한 코드만 로드하여 초기 로딩 시간 단축
    - 일반적으로 페이지 별로 코드 스플리팅을 구현
- 캐싱 전략
    - 서버 응답을 캐싱하여 동일한 요청에 대해 빠르게 응답할 수 있도록 함
    - Cache-Control 헤더를 설정하여 브라우저와 ODN에서 캐싱을 최적화stale-while-revalidate 등의 캐싱 전략을 통해 캐싱된 데이터를 사용하면서 백그라운드에서 새로운 데이터를 가져옴
- 리소스 최적화
    - 리소스 크기를 최적화하고 리소스가 필요할 때 로드되도록 함
    - WebP와 같은 현대적인 이미지 포맷을 사용하여 파일 크기를 줄임
- 최소화 및 번들링
    - Terser 플러그인을 사용하여 JavaScript 코드를 최소화
    - CSS와 JavaScript 파일을 별도로 분리하여 필요한 리소스만 로드

# 서버 통신 고급 기법

## 데이터 페칭 라이브러리(React Query, SWR)

- React Query
    - 서버 데이터를 쉽게 관리하고 캐싱하는 라이브러리
    - 요청의 상태 관리, 캐시 관리, 재시도 처리 등을 자동으로 처리
    - GraphQL, REST API 등 모든 종류의 백엔드와 통합하여 사용 가능
- SWR(Stale-While_Revalidate)
    - Next.js 팀에서 개발한 데이터 페칭 라이브러리
    - 캐시된 데이터를 보여주고 백그라운드에서 데이터를 다시 검증하여 업데이트
    - 데이터 요청을 최적화하여 성능 최적화

## 실시간 데이터 처리(WebSocket)

- 실시간 양방향 데이터 통신을 가능하게 하는 컴퓨터 통신 프로토콜
- HTTP와 달리 지속적 연결을 통해 데이터를 주고받을 수 있음
- WebSocket은 클라이언트와 서버 간 지속적인 연결 유지
- 이로 인해 서버 자원을 지속적으로 사용하므로 연결 관리와 리소스 사용에 주의해야함
- WebSocket 동작 과정
    - 클라이언트가 서버에 WebSocket 연결 요청
    - 서버는 요청을 수락하고 연결을 설정
    - 연결이 설정되면 양방향으로 데이터를 주고받을 수 있음
    - 클라이언트나 서버가 필요할 때 연결 종료 가능
- WebSocket 사용 예시
    - 실시간 채팅 : 사용자 간 메시지를 실시간으로 전송하고 받을 수 있음
    - 실시간 경고 및 알림 : 서버 측 데이터의 변화를 실시간으로 클라이언트에 알릴 수 있음

<img width="528" alt="image" src="https://github.com/user-attachments/assets/11ca51d3-817e-44de-be6d-e52ccf638744">

### WebSocket 장점

- 실시간성 : 데이터의 즉각적인 전달이 가능하여 실시간 앱 구현 가능
- 양방향 통신 : 클라이언트와 서버 간 데이터를 양방향으로 효율적 전송 가능
- 효율성 : HTTP보다 작은 오버헤드로 빠른 데이터 전송 가능

### WebSocket 단점

- 상태 관리 : 연결 상태를 유지하고 관리해야하며 연결 유지를 위한 추가적 처리 필요
- 보안 : HTTPS보다 추가적인 보안 설정 필요
- 호환성 : 일부 네트워크 환경에서 WebSocket을 지원하지 않을 수 있음

## WebSocket vs HTTP

### WebSocket

- 양방향 통신 가능
- 지속적 연결을 유지하고 데이터를 실시간으로 교환
- 실시간 채팅, 실시간 게임 등에 적합
- 바이너리 데이터 전송 가능

### HTTP

- 단방향 통신(클라이언트가 요청하고 서버가 응답)
- 비연결성 프로토콜이므로 각 요청마다 새로운 연결을 맺음
- 주로 웹 페이지 요청, 파일 전송 등에 사용
- 주로 텍스트 데이터를 전송하며 JSON, XML 등 다양한 형식을 지원
