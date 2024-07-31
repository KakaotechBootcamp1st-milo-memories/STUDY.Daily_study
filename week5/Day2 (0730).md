# 클린 코드의 정의와 중요성

## 클린 코드의 정의

### 간결하고 명확한 코드

- 클린 코드는 불필요한 복잡성을 제거하여 작성
- 이는 코드의 가독성을 높이고, 개발자가 코드를 빠르게 이해할 수 있도록 도와줌

### 읽기 쉬운 코드

- 클린 코드는 다른 개발자나 본인이 나중에 코드를 읽을 때 쉽게 이해할 수 있도록 작성
- 이를 위해 직관적인 변수명과 함수명을 사용하고, 코드 구조를 논리적으로 구성함

### 유지보수 가능한 코드

- 클린 코드는 수정 및 기능 추가가 용이하며, 버그 발생 가능성을 최소화함
- 이는 코드의 모듈화와 재사용성을 높이는 방식으로 달성됨

### 일관성 있는 코드

- 클린 코드는 일관된 코딩 스타일과 규칙을 준수함
- 이는 팀원 간의 협업을 원활하게 하고, 코드 리뷰 과정을 효율적으로 만듦

## 클린코드의 중요성

### 효율적인 개발

- 클린 코드는 읽기 쉽고 명확하기 때문에 개발 속도를 높이고, 버그를 줄여줌
- 이는 개발자들이 코드를 이해하고 수정하는 데 소요되는 시간을 줄여줌

### 유지보수 용이

- 클린 코드는 유지보수가 쉬워 새로운 기능을 추가하거나 기존 기능을 수정하는 데 용이
- 이는 장기적으로 프로젝트의 지속 가능성을 높임

### 협업 강화

- 여러 개발자가 협업하는 프로젝트에서 클린 코드는 팀원 간의 이해를 돕고, 코드 리뷰 과정에서 효율성을 높임
- 이는 팀의 생산성을 향상시키고, 코드 품질을 높이는 데 기여함

### 안정성 증가

- 명확하고 테스트 가능한 코드는 시스템의 안정성을 높이고, 예상치 못한 버그를 줄여줌
- 이는 사용자에게 신뢰성을 제공하고, 시스템의 가동 시간을 늘리는 데 기여함

### 비용 절감

- 유지보수와 수정에 드는 시간과 비용을 줄여줌으로써, 전체 프로젝트 비용을 절감하는 데 기여함
- 이는 프로젝트의 성공 가능성을 높이고, 자원을 효율적으로 활용할 수 있게 함

## 클린 코드 작성의 시간 투자로 장기적인 비용 절감

### 초기 시간 투자

- 클린 코드를 작성하면 변수명, 함수명, 일관된 코드 구조 작성의 필요로 인한 초기 시간이 더 소요됨

### 장기적인 비용 절감

- 시간이 지날수록 유지보수 비용이 크게 증가하지 않음
- 복잡하고 이해하기 어려운 코드의 문제를 미연에 방지
- 유지보수 비용 절감으로 전체 프로젝트 비용 절감

# 코드 스멜과 안티 패턴

## 코드 스멜의 개념

코드에서 나쁜 냄새가 난다는 의미로 명백한 버그는 아니지만 잠재적인 문제를 나타내는 코드의 징후를 말함

코드가 이해하기 어렵고 유지보수가 어렵거나 버그 유발 가능성이 높은 상태

### 대표적인 코드 스멜 유형

- Bloaters
- Object-Orientation Abusers
- Change Preventers
- Dispensables
- Couplers

## Bloaters

- 코드, 메서드, 클래스가 지나치게 커져서 다루기 힘든 상태를 말하며 시간이 지남에 따라 누적되는 경우가 많음
- 긴 메서드(Long Method)
- 큰 클래스(Large Class): 책임을 많이 가지고 있는 클래스
- 원시 집착(Primitive Obsession): 원시 타입을 과도하게 사용하는 경우
- 긴 매개변수 목록(Long Parameter List): 함수나 메서드의 매개변수가 너무 많아 사용하기 어려움
- 데이터 뭉치(Data Clumps): 여러 곳에서 함께 나타나는 데이터들이 그룹으로 다뤄지지 않고 분리되어 있는 경우

## Object-Orientation Abusers

- 객체 지향 프로그래밍 원칙이 불완전하거나 잘못 적용된 경우
- 대안 클래스들(Alternative Classes with nDifferent Interfaces): 유사한 가닝을 가진 클래스들이 다른 인터페이스를 사용하는 경우
- 거부된 상속(Refused Bequest): 서브 클래스가 상위 클래스의 메서드나 필드를 사용하지 않는 경우
- Switch문 (Switch Statements): 많은 조건 분기문이 사용된 경우
- 임시 필드(Temporary Field): 특정 상황에서만 값이 설정되는 필드가 있는 경우

## Change Preventers

- 한 곳의 변경이 여러 곳의 변경을 유발하는 경우를 말하며 소프트웨어 개발이 복잡해지고 유지보수 비용이 많이 들게 됨
- 변화 분산(Divergent Change): 하나의 클래스가 여러가지 이유로 자주 변경되는 경우
- 병렬 상속 계층(Parallel Inheritance Hierarchies): 하나의 클래스 계층에서 변경이 다른 계층에도 변경을 요구하는 경우
- 샷건 수술(Shotgun Surgery): 하나의 변경이 여러 클래스에 작은 변경을 요구하는 경우

## Dispensables

- 없어도 되는 코드로 제거하면 코드가 더 깨끗하고 효율적이 되며 이해하기 쉬워지는 경우
- 주석(Comments): 코드가 아닌 주석에 의존하여 설명이 필요한 경우
- 중복 코드(Duplicate Code): 동일한 코드가 여러 곳에 반복되어 유지보수가 어려움
- 데이터 클래스(Data Class): 데이터만 보유하고 메서드가 없는 클래스
- 죽은 코드(Dead Code): 더 이상 사용되지 않는 코드
- 게으른 클래스(Lazy Class): 하는 일이 거의 없는 클래스
- 추측성 일반화(Speculative Generality): 현재 필요하지 않지만 미래에 필요할 것 같아 추가된 코드

## Couplers

- 클래스 간 결합도가 지나치게 높거나 과도한 위임이 발생한 경우
- 기능 욕심(Feature Envy): 한 클래스가 다른 클래스의 기능을 지나치게 많이 사용하는 경우
- 부적절한 친밀성(Inappropriate Intimacy): 두 클래스가 서로의 내부에 지나치게 많이 접근하는 경우
- 불완전한 라이브러리 클래스(Incomplete Library Class): 필요한 기능이 부족한 라이브러리 클래스
- 메시지 체인(Message Chain): 여러 객체를 거쳐 메서드 호출이 일어나는 경우
- 중간자(Middle Man): 자신의 기능 없이 다른 객체로 작업을 위임하는 클래스

## 안티 패턴의 개념

- 일반적으로 좋지 않은 설계나 코딩 방식으로 특정 문제를 해결하기 위해 사용되었으나 오히려 더 많은 문제를 초래하는 방식

### 대표적인 안티 패턴

- 스파게티 코드: 코드가 복잡하게 얽혀있어 이해하기도 수정하기도 어려운 상태
- 갓 클래스: 하나의 클래스가 지나치게 많은 기능과 책임을 가지는 경우
- 골든 해머: 하나의 기술이나 방법을 과도하게 사용하여 모든 문제를 해결하려는 접근
- 레이지 초기화: 필요없어진 코드가 제거되지 않고 남아있는 상태
- 카고 컬트 프로그래밍: 패턴이나 방법을 그 목적이나 적합성을 이해하지 못한 채 단지 유행하거나 다른 프로젝트에서 사용되었다는 이유로 구현하는 것

## 코드 스멜과 안티 패턴을 피하는 방법

### 1. 코드 리뷰

- 정기적인 코드 리뷰를 통해 잠재적인 코드 스멜과 안티 패턴을 발견하고 수정

### 2. 정기적인 리팩토링

- 한 번에 많은 부분보다는 작은 단위로 자주 리팩토링

### 3. 명확한 설계와 문서화

- 설계 우선: 코딩하기 전 명확한 설계를 통해 코드 구조를 정의
- 문서화: 중요한 설계 결정과 코드 흐름을 문서화하여 팀원들과 공유

### 4. 지속적인 학습과 교육

- 최신 개발 기법과 패턴을 학습하고 이를 코드에 적용
- 정기적인 교육 세션을 통해 팀원들과 베스트 프랙티스 공유

### 5. 적절한 도구와 기술 사용

- 기술 적절성: 상황에 맞는 적절한 도구와 기술을 선택하여 사용
- 도구 평가: 사용 중인 도구와 기술을 정기적으로 평가하고 필요 시 업데이트하거나 교체

### 6. 기술 부채 관리

- 주기적으로 기술 부채를 평가하고 줄이기 위한 계획 수립
- 코드의 품질을 지속적으로 개선하여 기술 부채를 최소화

# 리팩토링의 개념과 필요성

## 리팩토링

- 기존 코드의 기능을 변경하지 않으며 코드 구조를 개선하는 과정
- 기능 동작은 그대로 유지하며 코드 구조를 개선하여 코드 가독성을 높이고 유지보수성을 향상시키고 중복을 줄이는 것을 목표로 함

## 필요성

- 코드 품질 향상 및 가독성 증가
- 유지보수성 증가
- 기능 추가 용이성
- 기술 부채 감소
- 팀 협업 향상

## 필요한 상황

- 코드 스멜 발견(긴 메서드, 중복 코드, 클 클래스 등)
- 새로운 기능 추가나 기존 변경 시(비즈니스 로직이 복잡하게 얽혀 있을 때, 새로운 기능을 추가하기 어려운 경우)
- 성능 문제(느린 데이터 처리, 비효율적인 알고리즘 등)
- 기술적 부채(임시방편적인 해결책이 남아있는 경우)
- 기존 코드의 비효율성(중복 로직이 분산되어 있는 경우)

# 클린 코드 작성 원칙

- KISS(Keep it Simple, Stupid): 코드를 단순하고 명확하게 작성
- DRY(Don’t Repeat Yourself): 중복되는 코드를 작성하지 않음
- YAGNI(Tou Aren’t Gonna Need It): 현재 필요하지 않은 기능은 구현하지 않음
- Principle of Least Astonishment: 코드의 동작이 직관적이고 예측 가능해야 함
- Boy Scout Rule: 코드를 수정할 때 항상 원래보다 더 깨끗하게 만들어 놓음

## 작성 원칙

### 1. 의미있는 이름 사용

- 명확하고 설명적인 이름 작성
- 의도를 분명히 밝이기
- 표준 명명 규칙 준수

### 2. 작고 단일 책임을 갖는 함수

- 함수는 하나의 작업만 수행
- 함수의 길이는 짧고 간결하게 유지
- 함수의 이름은 동사

### 3. 코드 중복 피하기

- DRY 원칙 준수
- 중복되는 코드는 함수나 클래스로 분리

### 4. 코드 형식 일관성 유지

- 팀이나 프로젝트의 코딩 스타일 가이드 준수
- 일관된 들여쓰기와 여백 사용

### 5. 에러 처리 잘하기

- 가능한 한 에러를 빠르게 감지하고 처리
- 예외 상황을 고려하여 코드를 작성

### 6. 가독성 높이기

- 코드의 가독성을 높이기 위해 의미 있는 곳에 공백을 사용
- 조건문과 반복문은 간결하고 명확하게 작성

### 7. 주석 사용

- 코드를 명확히 하기 위한 주석을 작성하되 불필요한 주석은 피함
- 복잡한 로직이나 의도가 명확하지 않은 부분에 설명 추가

# 주요 리팩토링 기법

## 함수 리팩토링

함수의 가독성과 재사용성을 향상시키고 단일 책임 원칙을 따름

### 함수 추출(Extract Function)

길고 복잡한 함수에서 일부 로직을 별도 함수로 분리

- 리팩토링 전

```bash
public void processOrder(Order order) {
    double discount = 할인 계산 로직
    double totalPrice = order.getPrice() - discount;
    // 기타 로직
}
```

- 리팩토링 후

```bash
public void processOrder(Order order) {
    double discount = calculateDiscount(order);
    double totalPrice = order.getPrice() - discount;
    // 기타 로직
}

private double calculateDiscount(Order order) {
    // 할인 계산 로직
    return discount;
}
```

### 함수 인라인(Inlining Function)

간단한 함수 로직을 호출 위치에 직접 삽입

- 리팩토링 전

```bash
public void displayMessage() {
    showMessage();
}

private void showMessage() {
    System.out.println("Hello, world!");
}
```

- 리팩토링 후

```bash
public void displayMessage() {
    System.out.println("Hello, world!");
}
```

### 매개변수 개수 줄이기

함수의 매개변수 개수를 줄이기 위해 데이터 구조 활용

- 리팩토링 전

```bash
public void createOrder(String productName, int quantity, double price) {
    // 주문 생성 로직
}
```

- 리팩토링 후

```bash
public void createOrder(OrderDetails details) {
    // 주문 생성 로직
}

public class OrderDetails {
    private String productName;
    private int quantity;
    private double price;
}
```

## 변수 및 상수 리팩토링

코드의 의미를 명확히 하고 하드코딩된 값을 상수로 변환

### 상수 추출(Extract Constant)

코드 내 하드코딩된 값을 상수로 정의

- 리팩토링 전

```bash
public void applyDiscount(double price) {
    double discount = price * 0.1;
}
```

- 리팩토링 후

```bash
private static final double DISCOUNT_RATE = 0.1;

public void applyDiscount(double price) {
    double discount = price * DISCOUNT_RATE;
}
```

### 변수 이름 변경(Rename Variable)

함수의 매개변수 개수를 줄이기 위해 데이터 구조를 활용

- 리팩토링 전

```bash
int t = 10;
```

- 리팩토링 후

```bash
int maxRetryCount = 10;
```

### 변수 범위 축소

변수의 유효 범위를 가능한 한 좁게 설정

- 리팩토링 전

```bash
public void processOrder() {
    double discount = 0;
    if (condition) {
        discount = calculateDiscount();
    }
    // 할인 적용 로직
}
```

- 리팩토링 후

```bash
public void processOrder() {
    if (condition) {
        double discount = calculateDiscount();
        // 할인 적용 로직
    } else {
        // 할인 적용 로직
    }
}
```

## 클래스 및 모듈 리팩토링

코드의 의미를 명확히 하고 하드코딩된 값을 상수로 변환

### 클래스 추출(Extract Class)

하나의 클래스가 너무 많은 책임을 지고 있을 때 새로운 클래스로 분리

- 리팩토링 전

```bash
public class OrderProcessor {
    private Customer customer;
    private Invoice invoice;

    public void createInvoice() {
        // 인보이스 생성 로직
    }
}
```

- 리팩토링 후

```bash
public class OrderProcessor {
    private Order order;
    private InvoiceCreator invoiceCreator;
}

public class InvoiceCreator {
    public void createInvoice(Order order) {
        // 인보이스 생성 로직
    }
}
```

### 클래스 병합(Merge Class)

서로 관련성이 높은 두 개 이상의 클래스를 하나의 클래스로 통합

- 리팩토링 전

```bash
public class Customer {
    private String name;
    private String address;
}

public class CustomerManager {
    public void updateCustomer(Customer customer) {
        // ...
    }
}
```

- 리팩토링 후

```bash
public class Customer {
    private String name;
    private String address;

    public void updateCustomer(Customer customer) {
        // ...
    }
}
```

### 변수 추출(Extract Variable)

복잡한 표현식을 설명 변수로 추출

- 리팩토링 전

```bash
double result = (height * width) - (2 * height + 2 * width);
```

- 리팩토링 후

```bash
double perimeter = 2 * (height + width);
double area = height * width;
double result = area - perimeter;
```

### 코드 정리(Clean Up Code)

불필요한 주석, 임시변수, 사용되지 않는 코드 등을 제거

- 리팩토링 전

```bash
public void processOrder(Order order) {
    // TODO: 주문 처리 로직 개선 필요
    if (order.isValid()) {
        // 사용되지 않는 코드
        System.out.println("Order is valid");
    }
    // 주문 처리 로직
}
```

- 리팩토링 후

```bash
public void processOrder(Order order) {
    if (order.isValid()) {
        // 주문 처리 로직
    }
}
```

### 조건문 단순화(Simplify Conditional Expressions)

복잡한 조건문을 단순하고 명확하게 재구성

- 리팩토링 전

```bash
if (isMember && hasPaid && !isExpired) {
    // ...
}

double getPayAmount() {
    double result;
    if (_isDead) result = deadAmount();
    else {
        if (_isSeparated) result = separatedAmount();
        else {
            if (_isRetired) result = retiredAmount();
            else result = normalPayAmount();
        }
    }
    return result;
}
```

- 리팩토링 후

```bash
if (isEligible()) {
    // ...
}

private boolean isEligible() {
    return isMember && hasPaid && !isExpired;
}

double getPayAmount() {
    if (_isDead) return deadAmount();
    if (_isSeparated) return separatedAmount();
    if (_isRetired) return retiredAmount();
    return normalPayAmount();
}
```

### 반복문 단순화

복잡한 반복문을 간단하게 만듦

- 리팩토링 전

```bash
for (int i = 0; i < items.length; i++) {
    process(items[i]);
}
```

- 리팩토링 후

```bash
for (Item item : items) {
    process(item);
}
```

### 죽은 코드 제거(Remove Dead Code)

더 이상 사용되지 않는 코드 제거

```bash
public void oldMethod(){
	// 미사용 코드 제거
}
```

### 매직 넘버 제거

코드 내 사용되는 매직 넘버를 의미있는 상수로 대체

- 리팩토링 전

```bash
double circumference = 2 * 3.14 * radius;
```

- 리팩토링 후

```bash
final double PI = 3.14;
double circumference = 2 * PI * radius;
```

# 코드 리뷰와 지속적인 개선

## 코드 리뷰 중요성

- 코드 품질 향상
- 지식 공유
- 일관성 유지
- 버그 예방
- 개발자 성장

## 지속적인 코드 개선이 필요한 이유

- 변화하는 요구사항에 대응
- 기술 발전에 대응
- 코드 품질 유지
- 팀 생산성 향상

## 지속적인 코드 개선 방법

- 정기적인 리팩토링
- 지속적인 통합(CI)
- 기술 부채 관리
- 최신 기술, 베스트 프랙티스의 교육과 학습
- 코드 리뷰 피드백 반영

## 코드 리뷰 방법

- 긍정적이고 건설적인 피드백 제공
    - 리뷰를 시작할 때는 긍적적인 부분부터 먼저 언급하고 문제를 지적할 때는 해결 방안도 함께 제시
- 명확하고 구체적인 피드백
    - 피드백에 대한 근거 제시, 문제점을 설명할 때는 코드 스니펫을 사용하여 시각적으로 이해를 도움
- 작은 단위로 자주 리뷰
- 정기적인 코드 리뷰 시간 할당
- 리뷰어와 작성자의 상호 존중
- 코드 리뷰 후 후속 조치
