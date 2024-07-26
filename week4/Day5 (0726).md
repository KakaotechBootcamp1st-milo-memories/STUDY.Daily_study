# 소프트웨어 테스트 중요성

## 테스트의 필요성

- 버그 조기 발견 및 수정
- 소프트웨어 품질 향상
- 개발 비용 절감
- 안정성 및 신뢰성 확보
- 사용자 만족도 증가

## 소프트웨어 테스트 유형

- 단위 테스트(Unit Testing): 개별 코드 단위의 기능 검증
- 통합 테스트(Integration Testing): 여러 모듈 간 상호작용 검증, 컴포넌트 간 인터페이스 및 데이터 흐름 확인
- 시스템 테스트(System Testing): 전체 시스템 기능과 성능 검증
- 인수 테스트(Acceptance Testing): 실제 운영 환경과 유사한 조건에서 사용자 관점으로 시스템 적합성 검증
- 성능 테스트(Performance Testing): 시스템 속도, 확장성, 안정성 검증, 부하테스트, 스트레스 테스트 등 포함

## 좋은 테스트의 특징(FIRST)

- Fast: 테스트는 빠르게 동작하여 자주 실행 가능해야함
- Independent: 각각의 테스트는 독립적이어야 함
- Repeatable: 어느 환경에서든 반복 가능해야 함
- Self-Validating: 테스트는 성공 또는 실패로 bool 값으로 결과를 내어 자체 검증되어야 함
- Timely: 테스트 코드는 테스트하려는 실제 코드를 구현하기 전 구현해야 함

# Mocking 이해하기

- Mocking은 테스트를 수행할 때 실제 시스템의 구성 요소를 대체하여 가짜 객체를 사용하는 기법
- 가짜 객체는 실제 객체와 유사한 인터페이스를 가지며 특정 동작이나 상태 모방 가능
- Mocking은 외부 시스템이나 의존성에 의존하지 않고도 테스트를 가능하게 함
- 실제 시스템의 구성 요소를 대체하여 테스트 환경을 제어 가능
- 테스트 대상 코드가 외부 시스템과의 상호작용없이 독립적으로 보장

## Mocking의 필요성

### 외부 의존성 영향 제거

- 실제 데이터베이스, API, 파일 시스템 등 외부 시스템 의존성을 제거
- 외부 시스템의 상태 변화나 네트워크 문제로 인한 테스트 실패 방지
- 개발 환경에 상관없이 일관된 테스트 결과 보장

### 테스트 속도 향상

- 외부 시스템과의 실제 상호작용 없이 테스트를 실행할 수 있어 테스트 속도가 빨라짐
- 대규모 시스템에서의 통합 테스트를 위한 시간을 단축 가능
- 가짜 객체를 사용함으로써 테스트의 실행 시간을 최소화하고 빠른 피드백 가능

### 테스트 일관성 유지

- 테스트 환경을 통제하여 일관된 결과 유지
- 외부 시스템의 가용성이나 상태의 영향을 받지 않으므로 동일한 테스트를 반복 실행해도 일관된 결과를 얻을 . 수있음

## Mocking, Stubbing

### Mocking: 행위 검증

- 가짜 객체 생성
- 가짜 객체의 동작을 미리 정의
- 실제 시스템의 상태 및 행동 모방
- 사용 예시: 데이터베이스 호출을 모킹하며 코드의 특정 로직 테스트
- **객체의 메소드 호출 여부와 호출 시 전달된 인수를 검증하여 특정 동작이 제대로 수행되었는지 확인**

```java
// Mocking: 메소드 호출 여부와 인수 검증
const mockCallback = jest.fn((x) => 42 + x);
[0, 1].forEach(mockCallback);

expect(mockCallback).toHaveBeenCalled(); // 호출 여부
expect(mockCallback.mock.calls.length).toBe(2); // 호출 횟수
expect(mockCallback.mock.calls[0][0]).toBe(0); // 인자값
expect(mockCallback.mock.calls[1][0]).toBe(1); // 인자값
```

### Stubbing: 상태 검증

- 특정 함수 호출 시 반환 값을 설정하거나 동작 정의
- 함수가 호출될 때마다 의도한 동작을 구현하도록 설정
- 의도한 결과를 얻기 위해 함수의 동작을 수정
- 사용 예시: 외부 API 호출을 스텁하여 특정 데이터나 에러 응답을 반환하도록 설정하여 테스트 진행
- **객체의 메소드 호출 시 반환될 값을 미리 설정하여 호출 결과에 따라 객체의 상태나 동작이 올바른지 검증**

```java
// Stubbing: 메소드가 반환한 상태값 검증
const mockCallback = jest.fn((x) => 42 + x);
[0, 1].forEach(mockCallback);

expect(mockCallback.mock.results[0].value).toBe(42);
expect(mockCallback.mock.results[1].value).toBe(43);
```

### → 엄밀히 말하면 둘은 다르지만 한 형태로 간주될 수 있음. 많은 경우 Mocking을 통해 Stubbing 기능도 함께 수행

# TDD와 BDD 소개

## TDD(Test-Driven Development)

테스트 주도 개발은 테스트 케이스를 먼저 작성한 이후 작성한 테스트 코드에 따라 실제 코드를 작성하는 방법

### 원칙: Red-Green-Refactor 사이클을 통해 개발

- Red: 실패하는 테스트를 작성
- Green: 테스트를 통과하는 최소한의 코드 작성
- Refactor: 중복 제거 및 코드 최적화

## BDD(Behavior-Driven Development)

- 행위 주도 개발은 사용자 행위를 기반으로 소프트웨어의 동작을 기술하고 검증하는 방법
- 사용자 행위를 기반으로 사용자 시나리오를 구성하여 테스트 케이스를 작성하고 개발하는 방법
- TDD에서 파생되었으며 TDD에서 기능 중심으로 테스트케이스를 작성하는데 한계를 극복하기 위해 등장

## 차이점

![image](https://github.com/user-attachments/assets/069e9b3a-3d5f-4314-9278-7cb9144d15f7)

### 목적

- TDD: 코드의 정확성을 검증, 버그를 줄이며, 리팩토링을 용이하게 함
- BDD: 사용자 요구사항을 중심으로 기능을 검증하고 이해 관계자와의 의사소통을 개선

### 접근 방식

- TDD: 개발자가 주로 테스트 코드를 작성
- BDD: 개발자, 테스트 담당자, 비즈니스 분석가가 협력하여 시나리오 작성

### 문서화

- TDD: 테스트 코드 자체가 문서 역할을 함
- BDD: 자연어 기반의 시나리오를 사용하여 문서화

## 장점

![image](https://github.com/user-attachments/assets/a7e87e83-1a31-4c8c-91f6-160377184ca5)

### TDD의 장점

- 코드 품질 향상
- 리팩토링 용이성
- 명확한 문서화

### BDD의 장점

- 이해관계자 간 소통 개선
- 요구사항 명확화
- 테스트 커버리지 향상

## 단점

- 높은 초기 비용
- 테스트 유지보수 부담: 코드 변경시 테스트 코드도 함께 수정
- 복잡한 테스트 작성: 복잡한 로직이나 외부 의존성이 많은 경우 테스트 작성이 어려움
- 잘못된 설계 유도 가능성: 과도한 테스트 작성으로 인해 코드 설계가 테스트 중심으로 왜곡될 수 있음

# TDD(Test-Driven Development)

## 기본 원칙: Red-Green-Refactor 사이클

### Red: 실패하는 테스트 작성

- 테스트 케이스를 작성하고 현재 구현된 코드가 테스트를 통과하지 못하도록 한다.
- 테스트는 기능에 대한 요구사항을 명확히 정의하며 실패함으로써 구현할 필요성을 강조

### Green: 테스트 통과를 위한 최소한의 코드 작성

- 코드는 빠르게 테스트를 통과하는데 집중하고 최적화나 구조적인 개선은 고려하지 않음

### Refactor: 코드 최적화

- 작성한 코드를 리팩토링하여 중복 코드 제거, 코드 품질 향상, 유지보수 용이성을 높임
- 모든 테스트가 통과하는지 확인하며 리팩토링 수행

### → 위 과정을 기능 구현이 완료될 때까지 반복

## TDD의 단계

### 테스트 작성

- 요구사항에 기반한 테스트케이스를 먼저 작성
- 테스트는 실패해야하며 이를 통해 개발할 기능을 명확히 함
- 테스트 케이스는 가능한 한 단순하고 명확하게 작성하여 구현할 기능의 목표를 구체적으로 제시

### 코드 작성

- 테스트를 통과하기 위한 최소한의 코드를 작성
- 코드는 테스트가 실패하지 않도록만 작성하고 기능 완성도는 고려하지 않음
- 작성한 코드는 나중에 리팩토링을 통해 개선될 수 있음을 염두에 둠

### 리팩토링

- 작성한 코드를 개선하여 가독성, 유지보수성을 높임
- 코드의 중복을 제거하고 코드 구조를 최적화
- 테스트가 성공적으로 통과하는지 확인하며 리팩토링 반복

### 테스트 코드 작성하기

- 테스트 케이스의 사전 준비/실행/테스트 검증을 나누어 작성
- 이는 테스트 메소드를 작성할 때 나타나는 패턴을 더 명확하게 표기해놓은 것으로 AAA pattern 혹은 GWT pattern이라고 부름
- assertEquals와 같은 assertion을 사용하여 예상 결과와 실제 결과를 비교

```java
import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.Test;

public class CalculatorTest {

    @Test
    public void add() {
        // Arrange / Given : 사전 준비
        Calculator calc = new Calculator();

        // Act / When : 함수 실행
        int result = calc.add(2, 3);

        // Assert / Then : 테스트 검증
        assertEquals(5, result);
    }
}
```

- 자바스크립트 jest에서는 describe를 통해 테스트를 그룹화하여 관리 가능
- test 혹은 it를 통해 개별 테스트 케이스를 정의 가능
- beforeEach, beforeAll, afterEach, afterAll 등을 통해 테스트 실행 전후에 특정 작업 수행 가능
- expect와 같은 assertion을 사용하여 예상 결과와 실제 결과를 비교

```java
const Calculator = require("./Calculator");

describe("Calculator", () => {
    let calc;

    beforeEach(() => {
        // Arrange / Given : 사전 준비
        calc = new Calculator();
    });

    test("add", () => {
        // Act / When : 함수 실행
        const result = calc.add(2, 3);

        // Assert / Then : 테스트 검증
        expect(result).toBe(5);
    });
});
```

### 테스트 코드 실행하기

- 실제 코드가 없으므로 테스트는 실패해야함
- 테스트 실패 내용을 분석하여 어떤 코드를 작성할지 설계
- 테스트 실패는 피드백 루프로 작용하여 요구사항을 정확히 반영하는 코드를 작성하도록 도와줌

### 실제 코드 작성하기

- 테스트를 통과하기 위한 최소한의 코드를 작성
- 코드는 테스트가 실패하지 않도록만 작성하고 기능 완성도는 고려하지 않음
- 작성한 코드는 나중에 리팩토링함을 염두에 둠

### 코드 리팩토링 및 반복

- 작성한 코드를 개선하여 가독성과 유지보수성을 높임
- 테스트가 성공하는지 확인하며 반복
- 리팩토링이 완료되면 기능 요구 사항에 대한 테스트 코드를 작성하고 과정 반복
- 이러한 과정을 Red-Green-Refactor 사이클이라 함

### 리팩토링의 원칙

- 작은 단계로 진행: 큰 변경보다는 작은 단위로 리팩토링을 진행
- 테스트 통과 유지: 리팩토링 과정에서 작성한 테스트가 모두 통과해야함
- 명확한 목표 설정: 리팩토링의 목적을 명확히 하고 코드 개선 방향 설정

```java
const Calculator = require("./Calculator");

describe("Calculator", () => {
    let calc;

    beforeEach(() => {
        calc = new Calculator();
    });

    test("add", () => {
        const result = calc.add(2, 3);
        const result2 = calc.add(13, 19);

        expect(result).toBe(5);
        expect(result2).toBe(32);
    });

    test("subtract", () => {
        const result = calc.subtract(5, 3);

        expect(result).toBe(2);
    });

    // ... 추가 테스트 코드 작성
});
```

## 테스트 코드 작성 요령

### 1. 가짜로 구현하기

- 테스트 코드를 통과만 할 수 있도록 실제 코드를 작성
- 그리고 테스트가 통과하면 단계를 거듭하며 코드를 발전시킴
- 최대한 빨리 테스트를 통과하는 것이 목적이며 복잡한 코드를 단계적으로 개발 가능
- 복잡한 코드에서는 이 방식으로 테스트 코드를 작성하는 것이 좋음

```java
// 테스트 클래스
const Calculator = require("./Calculator");

describe("Calculator", () => {
    test("add", () => {
        const calc = new Calculator();

        const result = calc.add(2, 3);

        expect(result).toBe(5);
    });
});

// 구현 클래스
class Calculator {
    add() {
        return 5;
    }
}
```

### 2. 삼각 측량

- 사전적 의미는 어떤 한 점의 좌표와 거리를 삼각형의 성질을 이용하여 알아내는 방법
- 즉, 2개의 정보를 통해 나머지 1개에 대한 정보를 알아내는 것
- 2개 이상의 예제를 작성하면 테스트는 실패할 것이고 테스트를 성공시키기 위해서는 실제 동작 코드를 일반화하여 구현

```java
// 테스트 클래스
const Calculator = require("./Calculator");

describe("Calculator", () => {
    test("add", () => {
        const calc = new Calculator();

        const result = calc.add(2, 3);
        const result2 = calc.add(19, 22);

        expect(result).toBe(5);
        expect(result2).toBe(41);
    });
});

class Calculator {
    add() {
        return 5;
    }
}

// 구현 클래스
class Calculator {
    add(a, b) {
        return a + b;
    }
}
```

### 3. 명백하게 구현하기

- 가짜로 구현하거나 삼각 측량 방법을 사용하지 않고 바로 정답을 구현하는 방법
- 쉽게 해결할 수 있는 문제는 바로 잘 동작하는 코드를 작성하는 것이 좋음

```java
const Calculator = require("./Calculator");

describe("Calculator", () => {
    test("add", () => {
        const calc = new Calculator();

        const result = calc.add(2, 3);

        expect(result).toBe(5);
    });
});

class Calculator {
    add(a, b) {
        return a + b;
    }
}
```

### 작성 요령 정리

- 가짜로 구현하기와 삼각 측량 방법은 복잡한 문제에 대한 테스트 코드를 작성하기 위한 작은 시작점
- 어떤 코드를 작성해야 하는지 명확하게 알고 있다면 문제를 빠르게 해결하는게 좋음
- 빠르게 해결 방법이 떠오르지 않는 경우, 가짜로 구현하기와 삼각 측량 방법을 통해 문제를 분할 정복하는 것이 핵심

### 백엔드 기능에 대한 테스트 코드 작성 순서

- Repository → Service → Controller 순서로 개발 진행
- Repository 계층의 테스트는 인메모리 데이터베이스 기반으로 테스트 진행
- Service 계층의 테스트는 Repository 계층을 Mock하여 진행
- Controller 계층의 테스트는 Service 계층을 Mock하여 진행
    - 자바의 경우 MockMVC를 활용하면 편리하게 구현 가능

## 실습예제로 TDD 살펴보기

### 요구사항

- 유저가 올바른 자격 증명을 입력하면 로그인 성공
- 잘못된 자격 증명을 입력하면 로그인 실패
- 유저가 로그인에 성공하면 인증 토큰 발급

### 실패하는 테스트 코드 작성

```java
 describe("Authentication", () => {
    const user = {
        id: "user_id",
        password: "user_password",
        token: "user_token",
    };

    test("올바른 자격 증명으로 로그인에 성공한다", () => {
        const result = login({ id: user.id, password: user.password });
        expect(result).toEqual({ success: true, token: user.token });
    });
});
```

### 테스트를 통과하는 코드 작성(가짜로 구현하기)

```java
const login = (username, password) => {
	return {success: true, token:"user_token");
};
```

### 테스트 코드 수정하기

```java
describe("Authentication", () => {
    test("올바른 자격 증명으로 로그인에 성공한다", () => {
        const result = login({ id: user.id, password: user.password });
        const result2 = login({ id: user2.id, password: user2.password });

        expect(result).toEqual({ success: true, token: user.token });
        expect(result2).toEqual({ success: true, token: user2.token });
    });
});
```

### 다시 테스트를 통과하는 코드 작성

```java
const users = [ ... ];

const login = (username, password) => {
    const user = users.find((u) => u.id === username && u.password === password);

    return { success: true, token: user.token };
};
```

### 다른 요구사항에 대한 테스트 코드 작성

```java
describe("Authentication", () => {
    test("올바른 자격 증명으로 로그인에 성공한다", () => {
        const result = login({ id: user.id, password: user.password });
        const result2 = login({ id: user2.id, password: user2.password });

        expect(result).toEqual({ success: true, token: user.token });
        expect(result2).toEqual({ success: true, token: user2.token });
    });

    test("잘못된 자격 증명으로 로그인에 실패한다", () => {
        const result = login({ id: user.id, password: "wrong" });

        expect(result).toEqual({ success: false });
    });
});
```

### 테스트를 통과하는 코드 작성

```java
const users = [ ... ];

const login = (username, password) => {
    const user = users.find((u) => u.id === username && u.password === password);

    if (user) {
        return { success: true, token: user.token };
    }
    return { success: false };
};
```

### 다른 요구사항에 대한 테스트 코드 작성

```java
describe("Authentication", () => {
    // ...

    test("잘못된 자격 증명으로 로그인에 실패한다", () => {
        const result = login({ id: user.id, password: "wrong" });

        expect(result).toEqual({ success: false });
    });

    test("유저가 로그인에 성공하면 인증 토큰을 받는다", () => {
        const result = login({ id: user.id, password: user.password });

        expect(result.success).toEqual(true);
        expect(result).toHaveProperty("token");
    });
});
```

## 테스트를 통과하는 코드 작성하기

```java
const generateToken = () => {
    // 토큰 발급 로직
    let token = "user_token";

    return token;
};

const login = (username, password) => {
    const user = users.find((u) => u.id === username && u.password === password);

    if (user) {
        return { success: true, token: generateToken() };
    }

    return { success: false };
};
```

# BDD(Behavior-Driven Development)

BDD는 사용자의 행위를 기반으로 사용자 시나리오를 구성하여 테스트케이스를 작성하고 개발을 진행하는 방식

BDD는 비 기술적 언어를 사용하여 더 많은 사람들이 쉽게 이해하도록 하며 고객과 개발자 관점에서 시스템이 어떻게 작동해야하는지에 초점을 맞춤

## BDD의 단계

### 1. 시나리오 작성

- 사용자 스토리: 사용자 관점에서 작성된 시나리오로 시스템이 어떻게 동작해야하는지 설명
- 자연어 사용: 시나리오는 기술적 용어를 지양하고, 자연어로 작성되어야 함
- 유스케이스 등 기획 단계에서 작성한 자료를 활용 가능

```java
Feature: 로그인 기능

Scenario: 유효한 자격 증명으로 로그인
    Given 사용자가 로그인 페이지를 방문했다
    When 사용자가 올바른 자격 증명을 입력하고 로그인 버튼을 클릭한다
    Then 사용자는 대시보드 페이지로 리디렉션된다
```

### 2. 테스트 작성

- 시나리오를 기반으로 구체적인 테스트 코드 작성
- TDD와 마찬가지로 AAA 혹은 GWT 패턴으로 테스트 코드를 작성

```java
describe("로그인 기능", () => {
    let currentPage;

    function visitLoginPage() {
        currentPage = "로그인 페이지";
    }

    function enterCredentials(username, password) {
        if (username === "user" && password === "pass") {
            currentPage = "대시보드 페이지";
        } else {
            currentPage = "로그인 실패 페이지";
        }
    }

    function clickLoginButton() {
        // 버튼 클릭 시 로그인 로직 수행
    }

    function getCurrentPage() {
        return currentPage;
    }

    test("유효한 자격 증명으로 로그인", () => {
        // Given
        visitLoginPage();
        expect(currentPage).toBe("로그인 페이지");

        // When
        enterCredentials("user", "pass");
        clickLoginButton();

        // Then
        expect(getCurrentPage()).toBe("대시보드 페이지");
    });
});
```

### 3. 실제 코드 작성

- 테스트를 통과하기 위한 최소한의 코드 작성
- 코드는 테스트가 실패하지 않도록만 작성하고 기능 완성도는 고려하지 않음
- 작성한 코드는 나중에 리팩토링을 통해 개선될 수 있음을 염두에 둠

## TDD와 BDD 비교

### TDD

- 코드 작성 전 테스트 코드를 먼저 작성
- Red-Green-Refactor 사이클을 따름
- 주로 유닛 테스트와 기능 테스트에 사용
- 개발자가 작성한 코드의 정확성 검증에 적합

### BDD

- 시스템 행동을 설명하는 테스트 작성
- 주로 수용 테스트와 통합 테스트에 사용
- 사용자 스토리와 요구 사항을 검증하는데 적합

## TDD를 선택하는 경우

- 코드의 정확성과 신뢰성이 중요한 프로젝트
- 코드 베이스가 복잡하고 유닛 테스트가 많이 필요한 경우
- 개발자가 TDD에 익숙하고 테스트 작성에 시간을 투자할 수 있는 경우

## BDD를 선택하는 경우

- 비즈니스 요구사항을 명확히 이해하고 검증해야하는 프로젝트
- 개발자와 비즈니스 이해관계자 간 협업이 중요한 경우
- 사용자 시나리오 기반 테스트가 필요한 경우

## 혼합 접근법

- 두 방법론의 장점을 결합하여 사용하는 경우도 많음
- 핵심 기능과 복잡한 로직에는 TDD를, 사용자 시나리오와 통합 테스트에는 BDD를 적용

## 테스트 작성 시 유의 사항

- 단일 책임 원칙 준수: 각 테스트는 하나의 동작만 검증
- 명확하고 간결하게 작성
- 테스트 독립성 보장: 테스트 간 의존성을 없애고 테스트 순서에 관계없이 동일 결과 보장
- 경계 조건 테스트: 정상적인 입력뿐만 아니라 경계 조건, 예외 상황 등도 테스트
- 실제 시나리오 고려: 실제 사용 시나리오를 반영하여 테스트 작성

# 테스트 자동화

테스트 케이스를 자동으로 실행하고 결과를 검증하는 프로세스

### 필요성

- 코드 변경 시마다 테스트를 자동으로 실행하여 신속한 피드백을 받기 위함
- 개발자의 수동 테스트 시간을 줄여 더 많은 시간동안 코드 작성에 집중할 수 있게 함
- 자동화된 테스트는 일관되게 실행되므로 사람의 실수를 줄이고 더 높은 품질의 소프트웨어 보장

## 주요 이점

- 시간과 비용 절약
- 빠른 피드백으로 버그 조기 발견
- CI/CD 프로세스를 원활하게 지원

## 테스트 자동화 도구 선택 시 고려사항

- 프로젝트 특성과 요구사항에 맞는 도구를 선택해야함
- 팀의 기술 스택과 학습 곡선 고려
- 장기적인 유지보수 용이성 염두

## 자동화 전략

### 테스트 피라미드 접근법

- 단위테스트를 기반으로 하는 계층적 전략
- 하위 레벨에 많은 테스트, 상위 레벨에 적은 테스트를 배치

### 중요 기능 우선 자동화

- 비즈니스 핵심 기능을 우선적으로 자동화
- 제한된 리소스로 최대 효과를 추구

### 반복적이고 시간 소모적인 테스트 자동화

- 수동 수행이 지루하고 시간이 많이 걸리는 테스트 자동화
- 테스터의 시간을 절약하고 창의적 테스트에 집중할 수 있게 함

## 테스트 자동화 도구

- Jenkins: 빌드, 테스트, 배포 자동화를 위한 오픈 소스 도구
- Travis CI: Github와 연동되는 호스팅된 CI 서비스
- CircleCI: 빠르고 간편한 CI/CD 서비스
- GitLab CI/CD: GitLab과 통합된 CI/CD 솔루션
- Github Actions: Github 푸시, 커밋 등 이벤트 트리거를 통해 테스트 실행
- husky, lint-stage: 자바스크립트 프로젝트에서 푸시, 커밋 등 작업을 수행하기 전에 테스트 실행
    - 자바에서는 pre-commit과 같은 패키지 사용 가능

## 테스트 자동화 방법: Git 커밋할 때 테스트하기

### Github Actions를 이용한 자동 테스트 설정

1. 프로젝트에 .github/workflows 디렉토리 생성

```java
$ mkdir -p .github/workflows
```

1. .github/workflows/ci.yml 파일을 생성하고 다음과 같이 작성

```java
name: CI

on: [push]

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      ...

      - name: Run tests
        run: ./gradlew test
```

### 자바스크립트 Husky와 lint-staged를 이용한 자동 테스트 설정

1. 프로젝트에 husky와 lint-staged 설치

```java
npm install --save-dev lint-staged husky
```

1. husky 설정

```java
npx husky install
npx husky add .huskt/pre-commit "npm run lint-staged"
```

1. lint-staged 설정
package.json 파일에 lint-staged 구성을 추가하여 커밋 시 실행할 스크립트 정의

```java
{
  "scripts": {
    "test": "jest"
  },
  "lint-staged": {
    "*.{js,ts}": ["npm test", "git add"]
  }
}
```
