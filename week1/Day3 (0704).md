# HTML5/CSS3/JS 기초

# HTML5

HTML5는 HTML의 최신 버전

- 시멘틱 요소 추가
- 비디오, 오디오 멀티미디어 기능 추가

## 기본 구조

- `<!DOCTYPE html>`: 문서가 HTML5로 작성되었음을 브라우저에 알림
- `<html>`: HTML 문서의 루트 요소로, 모든 콘텐츠를 감싸고 있음
- `<head>`: 이 태그 내에는 문서의 메타데이터, 제목, 스타일시트 링크 및 스크립트가 포함
- `<body>`: 이 태그 내에는 실제로 브라우저에 표시될 콘텐츠가 포함

## 기본 구조 직접 살펴보기

- 부라우저 실행 후 [F12]키를 눌러 개발자 도구 실행
- Elements(요소) 탭에서 페이지의 HTML 문서 형식 확인 가능

## HTML5 시멘틱 구조

HTML 요소를 사용하여 문서의 구조를 명확하게 정의하는 방법

단순한 스타일을 적용하기 위한 것이 아닌 문서의 의미를 명확히 하고 검색엔진이나 웹 크롤러가 문서를 이해하고 분석하는데 도움을 줌 → 이를 통해 웹 접근성을 높이고 SEO(검색 엔진 최적화)를 개선할 수 있음

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/5204d791-bc19-4179-81a7-1b1f0674b7ad)

→ 의미가 없는 <div>의 사용을 지양하고 최대한 의미가 있는 태그를 사용하는 것

### 주요 시멘틱 태그 종류

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/99c81cba-be01-411c-82c7-d2514c6b7bb8)

### HTML에서 자주 사용되는 태그

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/35c645b8-ead8-44a7-869e-18932ebc232c)

# CSS3(Cascading Style Sheets)

HTML이 웹 페이지의 구조를 담당한다면 CSS는 구조를 꾸며주는 역할

## 주요 역할

- 스타일 지정
- 레이아웃 조정 : Flexbox나 Grid와 같은 기술로 요소 정렬, 배치 가능
- 반응형 디자인 : 미디어 쿼리를 사용하여 다양한 디바이스 크기에 맞춰 웹 페이지를 반응형으로 만들 수 있음

## 기본 규칙

### 선택자(Selector)

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/d12bc6fa-8d6c-4058-bc47-faa5b7010724)

### 선택자(Selector)

CSS 선택자는 특정 HTML 요소를 선택하여 스타일을 적용하는 데 사용됩니다. 주요 선택자에는 전체 선택자(*), 요소 선택자, 클래스 선택자, ID 선택자가 있습니다.

- 전체 선택자 (*) : 문서 내의 모든 요소에 스타일을 적용할 때 사용

```css
* {
    margin: 0;
    padding: 0;
}
```

- 요소 선택자 : 특정 HTML 요소에 스타일을 적용할 때 사용

```css
p {
    color: blue;
    font-size: 16px;
}
```

- 클래스 선택자 : 특정 클래스 속성을 가진 요소에 스타일을 적용할 때 사용

```css
.header {
    background-color: #f0f0f0;
    padding: 20px;
}
```

- ID 선택자 : 고유한 ID 속성을 가진 요소에 스타일을 적용할 때 사용

```css
#main-title {
    font-size: 24px;
    font-weight: bold;
}
```

- 자식 선택자 : 특정 요소의 **직계 자식** 요소들을 선택하여 스타일 적용
    - 직계자식인 ul이 아닌 li요소들은 지정이 되지 않음
    - .container > li 는 불가 , .container > ul > li 는 가능

```css
<div class = "container">
	<ul>
		<li>항목1</li>
		<li>항목1</li>
		<li>항목1</li>
	</ul>
</div>
```

```css
.container > ul{
	padding:10px
}
```

- 자손 선택자 : 특정 요소의 자손 요소들을 선택하여 스타일을 적용

```css
.container li {
	padding : 10px
}
```

## 레이아웃

### 박스 모델

HTML 요소는 content, padding, border, margin으로 구성

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/3ac7aa91-b200-4e92-ae16-5e0b9eea42a0)

- content: 실제 내용이 표시되는 영역입니다.
- padding: 내용과 테두리 사이의 내부 여백입니다.
- border: 요소의 테두리를 형성하는 영역입니다.
- margin: 요소의 테두리 바깥쪽의 외부 여백입니다.

### 플렉스 박스

요소를 효율적으로 정렬, 배치할 수 있는 레이아웃 모델으로 주로 한방향으로 요소들을 정렬하는데 사용

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/bf2ee7b5-655d-44e0-ac1d-0b5184294c4d)

css에서 `display: flex`로 부모 요소를 플렉스 컨테이너로 만들고 자식요소를 유연하게 배치가능

### Grid

2차원 레이아웃 시스템으로 요소들을 행과 열의 격자 모양으로 배치할 수 있다.

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/327c6ccd-5e3d-4e27-8ec8-cf0ef0593604)

`display: grid;`를 사용하여 그리드 컨테이너를 만들고 각 요소들을 그리도 셀에 배치

반응형 웹디자인에 유용

### floating

특정 요소를 화면 한쪽에 띄우는 레이아웃

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/e636cd09-9400-434a-b365-29a217e0d421)

## 알아두면 좋은 용어

- **반응형 디자인(Responsive Design)**: 다양한 디바이스와 화면 크기에 맞춰 웹 페이지가 자동으로 레이아웃과 콘텐츠를 조절하는 디자인 기법
- **웹 접근성(Web Accessibility)**: 장애를 가진 사람들을 포함하여 모든 사용자가 웹 콘텐츠를 쉽게 접근하고 사용할 수 있도록 보장하는 기술과 원칙
- **크로스 브라우징(Cross-browser Compatibility)**: 웹 페이지가 다양한 웹 브라우저에서 일관되게 표시되고 작동할 수 있도록 보장하는 기술과 방법

# JavaScript

웹 페이지의 다양한 기능을 만들어주는 프로그래밍 언어, 웹 페이지가 사용자와 상호작용하고 동작을 제어하는데 사용됨

- 이벤트 처리 : 마우스 동작 등의 이벤트를 감지하고 동작 수행
- 웹 페이지 조작 : HTML 요소를 동적으로 변경하여 사용자 경험 개선
- 데이터 처리 : 서버와의 데이터 교환, 데이터 유효성 검사 등으로 데이터 처리 담당

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/f886a994-9759-4be8-a3de-a80457dfe419)

### 기본 속성

- 동적 타입 언어 : 변수의 타입을 선언하지 않고 사용할 수 있으며 runtime에 타입이 정해짐
- 인터프리터 언어 : 코드를 한 줄씩 해석하고 실행
- 객체 기반 언어

### 기본 문법

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/5d88cadf-9b19-4651-99b7-ec90037709e3)

- 변수 선언

```jsx
// let 키워드: 변수 재할당은 가능하지만 재선언은 불가
let y = 30;
y = 40; // 재할당 가능

// const 키워드: 변수 재선언과 재할당 모두 불가
const z = 50;

```

- 함수 선언

```jsx
// 함수 선언식
function add(a, b) {
  return a + b;
}

// 함수 표현식
const subtract = function(a, b) {
  return a - b;
};

// 화살표 함수 (ES6)
const multiply = (a, b) => {
  return a * b;
};

```

- 객체 선언

```jsx
const person = {
  name: "milo",
  age: 26,
  hello: function() {
    console.log("Hello, " + this.name);
  }
};

// 객체에 접근 및 메서드 호출
console.log(person.name); // John
person.hello(); // Hello, John

```

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/24523b0d-b61d-4451-b89a-9486a602ab9f)

## ES6+ JS

ES6+는 JS의 최신 버전(ECMAScript 2015 이후 버전)들을 통칭하는 용어

## DOM(Document Object Model) 조작 기초

HTML 문서의 구조화된 표현을 제공하며 이를 프로그래밍 언어가 이해하고 조작할 수 있게 해주는 인터페이스, 즉, 웹 페이지의 요소들을 트리 구조로 표현하여 해당 요소를 수정하고 접근할 수 있다.

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/df717c13-5e3c-400f-945b-7d6ca0c0c761)

DOM을 통해 웹 페이지의 내용을 동적으로 수정하고 사용자와의 상호작용을 구현할 수 있다.

### DOM 요소

`document` 객체는 현재 브라우저에 로드된 전체 HTML 문서를 나타내며, DOM을 조작할 수 있는 기본 인터페이스를 제공합니다.

```jsx
// DOM 요소 선택
let heading = document.querySelector('h1');

// 요소의 텍스트 내용 변경
heading.textContent = '새로운 제목';

// 새로운 요소 생성
let newParagraph = document.createElement('p');
newParagraph.textContent = '이것은 새로운 문단입니다.';

// 기존 요소에 새로운 요소 추가
document.body.appendChild(newParagraph);

// 이벤트 리스너 추가
heading.addEventListener('click', () => {
  alert('제목이 클릭되었습니다!');
});

```

### 이벤트 처리

addEventListener는 지정한 이벤트를 감지하고 그 떄 실행할 함수를 정의하는 역할

- EventType : click. dbclick, keydown, mousemove, mouseover, change 등
- callback : 이벤트가 발샐했을 때 실행할 함수, 이벤트 처리 외에도 타이머 함수, HTTP 요청, 파일 처리 등 다양한 상황에서 활용
- 이는 비동기로 동작

## 비동기(Asynchronous)

프로그래밍에서 특정 작업이 다른 작업의 완료를 기다리지 않고 독립적으로 실행되는 방식

특히 네트워크 요청, 파일 읽기/쓰기, 데이터베이스 쿼리 등의 I/O 작업에서 중요한 개념

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/62a90ad4-af1f-4ba5-8347-1112812250d0)

### 비동기 동작의 특성

- **동시성**: 여러 작업을 동시에 처리하는 개념으로, 비동기 작업은 다른 작업이 완료될 때까지 기다릴 필요 없이 병렬로 실행
- **비차단**: 비동기 작업은 다른 작업을 방해하지 않고 독립적으로 실행되며, 작업이 완료될 때까지 다른 코드의 실행을 차단하지 않음
- **콜백 함수**: 비동기 작업이 완료되었을 때 호출되는 함수로, 작업 완료 후 실행할 코드를 정의하여 비동기 작업의 결과를 처리

### 콜백 함수의 문제점

- 콜백 지옥 **:** 다중 중첩된 콜백 함수들로 인해 코드가 매우 복잡해지고 가독성이 떨어지는 현상
- 에러 처리 어려움 : 에러가 발생했을 때 각 콜백마다 별도로 에러 처리를 구현해야 하며, 에러가 전파되는 과정에서 예상치 못한 문제를 발생시킬 수 있습니다.

### Promiss와 async/await

프로미스는 비동기 작업의 완료 또는 실패를 나타내는 객체, 프로미스를 사용하면 비동기 작업이 끝났을 때 어떤 동작을 수행할지 지정할 수 있음

- Promise의 세가지 상태
    - 대기
    - 이행
    - 거부

```jsx
// Promise 예시
let myPromise = new Promise((resolve, reject) => {
  let success = true;

  if (success) {
    resolve("작업이 성공적으로 완료되었습니다!");
  } else {
    reject("작업이 실패했습니다.");
  }
});

// Promise 사용 예시
myPromise
  .then((message) => {
    console.log(message); // 작업이 성공적으로 완료되었을 때 실행
  })
  .catch((error) => {
    console.error(error); // 작업이 실패했을 때 실행
  });

```

async/await는 promiss를 보다 쉽게 사용할 수 있도록 도와주는 문법

```jsx
// async/await 예시
function fetchData() {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      const success = true; // 이 값을 true 또는 false로 변경하여 테스트할 수 있습니다.

      if (success) {
        resolve("데이터를 성공적으로 가져왔습니다");
      } else {
        reject("데이터 가져오기에 실패했습니다");
      }
    }, 2000);
  });
}

async function getData() {
  try {
    const data = await fetchData();
    console.log(data); // 데이터가 성공적으로 가져와졌을 때 실행
  } catch (error) {
    console.error(error); // 데이터 가져오기에 실패했을 때 실행
  }
}

getData();

```

- Promise는 비동기 작업의 성공 또는 실패를 나타내는 객체로, then과 catch를 통해 결과를 처리
- async/await는 Promise를 보다 간단하게 사용할 수 있게 해주는 문법으로, 코드의 가독성을 높여줌
- async 키워드를 함수 앞에 붙이고, await 키워드를 비동기 작업 앞에 사용하여 동기식 코드처럼 작성 가능
