# 리액트와 타입스크립트

## 타입스크립트 기초

### 자바스크립트 동적 타입의 문제점

자바스크립트는 동적 타입 언어로 유연성과 편리함을 제공하지만 아래과 같은 문제점 발생 가능

- 런타임 에러 발생 가능성
- 타입 불일치 문제
- 유지보수의 어려움

### 타입스크립트 개요

자바스크립트의 상위 집합 언어로 정적 타입 언어 기능을 제공하는 언어

![image](https://github.com/KakaotechBootcamp1st-milo-memories/STUDY.Daily_study/assets/102672547/f227ad1c-2e66-4303-bc69-b9c8eab3787a)

### 주요 특징

- 자바스크립트 호환성 : 기존 자바스크립트 코드를 그대로 사용 가능
- 정적 타입 사용 : 변수, 매개변수, 반환 값 등에 명확한 타입을 지정하여 사전에 오류를 방지할 수 있음
- 타입 추론 기능 : 초기화된 변수 타입을 자동으로 추론하는 기능이 있어 개발자가 모든 변수에 타입을 정의하지 않아도 된다.

### 타입스크립트의 장점

- 코드 안정성과 신뢰성
- 가독성과 유지보수성
- 타입 확장성 : 자체 타입 시스템을 활용하여 복잡한 데이터 구조나 비즈니스 로직을 효율적으로 모델링 가능

### 타입스크립트의 단점

- 트랜스파일링 단계 추가 : 자바스크립트로 변환하는 트랜스파일링 단계가 추가되므로 빌드 시간이 길어질 수 있다.
- 복잡성 증가 : 자바스크립트의 장점이 빠른 학습이었지만 타입스크립트를 도입하면 초기 학습 곡선이 존재한다.
- 타입 선언 관리 : 외부 라이브러리나 모듈을 사용할 때 해당 라이브러리의 타입 정의 파일이 필요할 수 있다.

### 기본 타입

- boolean : `let isDone:boolean = false;`
- number : `let num:number = 10;`
- string : `let name:string = "John";`
- Array : `let list:number[] = [1, 2, 3];`
- Tuple : `let x:[string, number] = ["hello", 10];`
- Enum : `enum Color {Red, Green, Blue};`
- any : 모든 타입을 가질 수 있음. 컴파일 타임에 타입 검사를 피하고 싶을 때 사용
    - `let notSure: any = 4;`
- void : `function warnUser(): void { console.log("This is a warning message"); }`
- null/undefined : 기본적으로 모든 타입의 하위 타입
    - `let u: undefined = undefined;`
    - `let n: null = null;`
- 사용 예시

```jsx
let age = 30;
age = "서른"; //불가능(타입 추론 기능으로 타입 자동 추론)

let age:number = 30;
age = "서른" //타입에러 발생
```

- 함수에 타입 사용하기

### 함수에 타입 사용하기

타입스크립트에서는 함수의 매개변수와 반환 값에도 타입을 지정할 수 있습니다.

간단한 예시:

```tsx
function add(x: number, y: number): number {
  return x + y;
}

let result = add(2, 3); // result는 5

```

선택적 매개변수 예시:

```tsx
function greet(name: string, greeting?: string): string {
  if (greeting) {
    return `${greeting}, ${name}!`;
  } else {
    return `Hello, ${name}!`;
  }
}

let greet1 = greet("John"); // "Hello, John!"
let greet2 = greet("John", "Good morning"); // "Good morning, John!"
```

### 타입 별칭 만들기

- 기존 타입에 새로운 이름을 지어주는 기능으로 복잡한 타입을 간결하게 표현할 수 있고 코드 가독성을 높일 수 있다.

```tsx
type User = {
  name: string;
  age: number;
  email: string;
};

let user: User = {
  name: "John Doe",
  age: 30,
  email: "john.doe@example.com"
};
```

### 유니온 타입

두 개 이상의 타입을 허용하는 타입

```jsx
type Status = "active"|"inactive";
let userStatus : Status = "block" //error
```

### 인터섹션 타입

```jsx
type User = {
  name: string;
  age: number;
  email: string;
};

type Person = {
  name: stringl
  address: string;
  phone_num: string;
};

type Capt = User&Person
```

### 인터페이스 만들기

타입을 정의하는 또 다른 방법으로 클래스나 객체가 반드시 구현해야하는 구조를 명시 가능

간단한 인터페이스 예제:

```tsx
interface User {
  name: string;
  age: number;
  email: string;
}
```

### Type vs Interfaces

- 확장성 : 인터페이스는 나중에 새 속성을 추가할 수 있지만 타입은 생성 후 변경할 수 없음
- 선언 병합 : 인터페이스는 선언 병합을 지원하지만 타입 별칭은 불가능
    - **Type**: 타입은 선언 병합을 지원하지 않습니다. 동일한 이름으로 여러 번 선언할 수 없음
    - **Interface**: 인터페이스는 선언 병합을 지원, 동일한 이름의 인터페이스를 여러 번 선언하면 하나로 병합
        
        ```tsx
        interface User {
          name: string;
        }
        interface User {
          age: number;
        }
        // User 인터페이스는 name과 age 프로퍼티를 가집니다.
        ```
        
- 사용 범위
    - **Type**: 타입은 기본 타입, 유니온 타입, 튜플 등 다양한 타입 표현에 사용됩니다.
        
        ```tsx
        type ID = string | number;
        type Pair = [number, number];
        ```
        
    - **Interface**: 인터페이스는 객체의 구조를 정의하는 데만 사용됩니다.
        
        ```tsx
        interface User {
          name: string;
          age: number;
        }
        ```
        

### Type과 Interface의 사용 시기

- **Type을 사용**
    - 기본 타입, 유니온 타입, 튜플 등 다양한 타입을 정의할 때
    - 복잡한 타입을 간결하게 표현하고 싶을 때
- **Interface를 사용**
    - 객체의 구조를 정의할 때
    - 클래스나 객체가 반드시 구현해야 하는 구조를 명시할 때
    - 선언 병합이 필요한 경우
    - 확장성이 요구되는 경우 (나중에 새로운 속성을 추가할 수 있음)

# 타입스크립트 고급 활용

## 제네릭 사용

제네릭은 타입스크립트에서 코드 재사용성을 높이고 타입 안전성을 유지할 수 있다.

제네릭은 함수, 클래스, 인터페이스, 타입 별칭 등에 적용할 수 있고, 트랜스파일링 타임에 타입이 결정됨

### 제네릭 함수 선언

제네릭 함수는 함수의 입력이나 출력 타입을 호출 시점에 지정할 수 있게 함

```tsx
function identity<T>(arg: T): T {
  return arg;
}

let output1 = identity<string>("Hello"); // "Hello"
let output2 = identity<number>(123); // 123

```

### 제네릭 인터페이스 선언

제네릭 인터페이스는 인터페이스의 일부 또는 전체를 제네릭 타입으로 정의할 수 있게 함

```tsx
interface Box<T> {
  contents: T;
}

let stringBox: Box<string> = { contents: "Hello" };
let numberBox: Box<number> = { contents: 123 };

```

### 제네릭 제한 조건

제네릭 타입 매개변수에 특정 타입을 확장하도록 제한을 줄 수 있음.

```tsx
interface Lengthwise {
  length: number;
}

function logLength<T extends Lengthwise>(arg: T): T {
  console.log(arg.length);
  return arg;
}

logLength({ length: 10, value: "Hello" }); // 10
// logLength(3); // 오류: 'number' 형식에 'length' 속성이 없습니다.

```

`logLength` 함수는 제네릭 타입 `T`를 받지만, `T`는 `Lengthwise` 인터페이스를 구현해야 하므로 `length` 속성을 가진 객체만 함수에 전달할 수 있음

### 타입 가드

런타입에서 타입을 좁히기 위해 사용

1. 사용자 정의 타입 가드

개발자가 직접 정의하는 함수를 통해 타입을 좁힘

is키워드를 사용한 타입 서술어를 반환 타입으로 사용

간단한 예제:

```tsx
function isFish(pet:Fish|Bird): pet is Fish{
  return (pet as Fish).swim !== undefined;
}

if (isFish(pet)) {
  pet.swim(); //여기서 pet은 Fish타입으로 추론됨
}
```

1. in 연산자 타입 가드

객체에 특정 프로퍼티가 존재하는지 확인하여 타입을 좁힘

```jsx
function move(pet:Fish|Bird){
	if("swim" in pet){
		return pet.swim(); //여기서 pet은 Fish타입으로 추론됨
	}
	return pet.fly() //여기서 pet은 Bird타입으로 추론됨
}
```

1. typeof 타입 가드

```jsx
function padLeft(value:string, padding:string|number){
	if (typeof padding === "number"){
		return Array(padding+1).join(" ") +value;
	}
	return padding + value // 여기서 Padding은 string타입으로 추론됨
}
```

1. instanceof 타입 가드

```jsx
if (padder instanceof SpaceRepeatingPadder{
	padder.numSpaces; // padder는 SpaceRepeatingPadder로 추론됨
}
```

### 타입 가드의 장점과 주의사항

- 타입 가드의 장점
    - 코드 타입 안전성 향상
    - 런타임 오류 감소
    - IDE 자동 완성 기능 개선
    - 코드 가독성 및 유지 보수성 향상
- 주의 사항
    - 과도한 사용은 코드 복잡성을 증가시킴
    - 런타임 체크로 인한 성능 영향을 고려해야함.

### 타입 유틸리티

코드의 가독성과 유지보수성을 높이기 위해 새로운 타입을 쉽게 생성할 수 있도록 함

- Partial : 모든 프로퍼티를 선택적으로 만듦
- Record : 특정 키 타입과 값 타입을 가진 객체 타입을 만듦

# 리액트와 타입스크립트

## 타입 에러 해결 및 디버깅

### 일반적인 타입 에러 유형

1. 타입 불일치 에러 
2. Null 또는 Undefined 에러
3. 존재하지 않는 프로퍼티 접근 에러 
    
    ```jsx
    let user = {name:"milo"};
    console.log(user.age); // error
    ```
    
4. 함수 인자 타입 에러

### 해결 방법

**명시적 타입 캐스팅**

- 타입스크립트에서 변수나 표현식의 타입을 개발자가 명시적으로 지정하는 것
- 일반적으로 타입스크립트가 자동으로 타입을 추론할 수 없는 복잡한 경우나 다양한 타입 간 변환 시 사용됨
- 과사용은 타입 안정성을 저해시킴

```jsx
let someValue : any = "this is a string";
let strLength:number = (<string>someValue).length; // Angle Bracket 문법
let strLength:number = (someValue as string).length; //as문법
```

### 디버깅

- 타입 추론 오류 확인
- 타입스크립트 설정 검토
- 타입 에러 메시지 이해
- 타입스크립트 디버거 사용

## 타입스크립트 작성 시 주의 사항

- 명확한 타입 정의
- 타입 추론 이용
- 타입 에러 처리
- 타입스크립트 최신 기능 활용
- any 타입 사용 금지
