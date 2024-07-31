# 디자인 패턴

## 디자인 패턴의 정의

소프트웨어 개발 과정에서 공통적으로 자주 발생하는 문제들에 대한 재사용 가능한 해결책

구체적인 구현이 아닌 문제 해결을 위한 템플릿이며 객체 지향 설계 원칙을 따른다.

## 디자인 패턴의 중요성

- 개발 시간의 단축
- 코드 품질 향상
- 확장성 확보
- 의사소통 개선
- 재사용성 증대
- 복잡성 관리
- 모범 사례 적용

# 주요 백엔드 디자인 패턴

MVC(Model=View-Controller) 패턴

앱을 세가지 주요 컴포넌트로 분리하는 아키텍쳐 패턴

사용자 인터페이스와 비즈니스 로직을 분리하여 유지보수성, 확장성 향상

- Model: 데이터와 비즈니스 로직을 관리
- View: 사용자에게 정보를 표시
- Controller: Model과 View 사이의 상호작용을 조정

<img width="411" alt="image" src="https://github.com/user-attachments/assets/9f0fef7c-02e5-45c1-9fc6-f99ce0dff704">

### 프로세스 흐름

1. 사용자가 View를 통해 백엔드 서버로 요청을 보냄
2. 서버의 Controller가 요청을 받아 처리
3. Controller가 필요시 Model을 업데이트
4. Model이 변경되면 View에 반영
5. 업데이트된 View가 사용자에게 표시

### 장점

관심사 분리로 코드 유지보수 용이

각 컴포넌트의 독립적인 개발 가능

테스트 용이성 증가

### 단점

복잡한 앱에서는 컨트롤러 비대 가능성

세가지 주요 컴포넌트 역할과 상호작용을 명확히 이해해야 함

## MVC 변형 패턴

### MVP(Model-View-Presenter) 패턴

### 개요

MVC의 Controller를 Presenter로 대체한 패턴

View와 Model의 완전한 분리가 특징

### 구성

Model: 데이터와 비즈니스 로직 관리

View: 사용자 인터페이스, Presenter와 1:1관계

Presenter: View와 Model 사이의 중재자 역할

### 특징

View와 Model 간 직접 통신 없음

Presenter가 View와 Model 모두 참조

테스트 용이성 증가

### MVVM(Model-View-ViewModel) 패턴

### 개요

주로 UI 개발에 사용되는 패턴

데이터 바인딩을 활용한 View와 ViewModel의 느슨한 결합이 특징

### 구성

Model: 데이터와 비즈니스 로직 관리

View: 사용자 인터페이스

ViewModel: View를 위한 Model 표현, View와 Model 사이의 중재자

### 특징

데이터 바인딩으로 View와 ViewModel 간 자동 동기화

View의 상태와 동작을 VIewModel에서 관리

UI플랫폼 독립적인 개발 가능

<img width="411" alt="image" src="https://github.com/user-attachments/assets/e48589d7-dd63-46bd-b5a1-330c9b5bc1fa">

## MVC vs MVP vs MVVM

### 데이터 흐름

- MVC: Controller → Model → View
- MVP: Model ↔ Presenter ↔ View
- MVVM: Model → ViewModel ↔ View(양방향 데이터 바인딩)

### View와 Model의 결합도

- MVC: 중간
- MVP: 낮음
- MVVM: 매우 낮음

### 사용 상황

- MVC: 일반적인 웹 앱
- MVP: 복잡한 UI 로직을 가진 앱
- MVVM: 데스크톱 또는 모바일 앱, SPA

## 싱글톤 패턴

클래스의 인스턴스가 오직 하나만 생성되도록 보장하는 디자인 패턴

전역 접근 지점을 통해 어디서든 인스턴스에 접근 가능

리소스 공유, 상태 관리 등에 주로 사용

### 구현 방법

1. 생성자를 private으로 선언
2. 클래스 내부에 자신의 정적 인스턴스를 보관
3. 인스턴스에 접근…

```jsx
Public class Singleton{
	private static Singleton inst;
	
	private Singleton() {
			//생성자 코드
	}
	
	public static Singleton getInst(){
		if (inst == null){
			inst = new Singleton();
		}
		return instance;
	}
}
```

### 장점

- 단일 인스턴스 보장: 클래스의 인스턴스가 하나만 생성되므로 메모리와 리소스 절약 가능
- 전역적 접근
- 지연된 초기화: 필요한 시점에서 인스턴스를 생성하므로 초기화 과정이 지연되어 성능 향상 가능

### 단점

- 멀티 스레드 환경에서 동기화 문제: 동시에 여러 스레드에서 접근할 경우 인스턴스 상태가 일관성 없이 될 수 있으므로 동기화 처리 필요
- 테스트 어려움: 전역 상태를 유지하는 패턴이기 때문에 테스트 시 의존성 관리가 어려울 수 있음
- 단일 책인 원칙 위배 가능성: 너무 많은 책임을 맡게 되면 클래스의 책임이 모호해질 수 있음

### 사용 사례

- 커넥션 풀 관리: 데이터베이스와 연결과 같은 공유 자원을 단일 인스턴스로 관리할 때 유용
- 설정 정보 관리: 시스템 설정 정보나 로그 기록과 같은 공유 데이터를 처리할 때 사용할 수 있음
- 캐시 관리: 여러 곳에서 접근되는 캐시 객체를 싱글톤으로 관리하여 일관된 데이터 접근을 보장 가능

## 팩토리 패턴(Factory Pattern)

객체를 생성하는 인터페이스를 정의하고 이를 통해 객체의 생성을 서브 클래스에게 위임하는 디자인 패턴

이 패턴을 사용하면 실제 생성되는 객체의 클래스를 몰라도 되며 추상적인 인터페이스나 추상 클래스를 통해 객체를 생성하고 이를 반환받을 수 있음

### 구성 요소

- 추상 팩토리: 객체 생성을 위한 인터페이스 제공, 팩토리 메서드 패턴과는 달리 객체의 구체적인 클래스를 지정하지 않음
- 구체적 팩토리: 실제 객체를 생성하는 클래스
- 제품: 생성되는 객체

```jsx
// AnimalFactory 인터페이스
public interface AnimalFactory {
    Animal createAnimal();
}

// 개를 생성하는 구체적 팩토리 클래스
public class DogFactory implements AnimalFactory {
    @Override
    public Animal createAnimal() {
        return new Dog();
    }
}

// 고양이를 생성하는 구체적 팩토리 클래스
public class CatFactory implements AnimalFactory {
    @Override
    public Animal createAnimal() {
        return new Cat();
    }
}

// 제품 클래스 - Animal 인터페이스 구현체
public interface Animal {
    void makeSound();
}

// 구체적인 제품 클래스 - Dog
public class Dog implements Animal {
    @Override
    public void makeSound() {
        System.out.println("멍멍!");
    }
}

// 구체적인 제품 클래스 - Cat
public class Cat implements Animal {
    @Override
    public void makeSound() {
        System.out.println("야옹!");
    }
}

// 테스트 클래스
public class FactoryPatternTest {
    public static void main(String[] args) {
        AnimalFactory dogFactory = new DogFactory();
        Animal dog = dogFactory.createAnimal();
        dog.makeSound();

        AnimalFactory catFactory = new CatFactory();
        Animal cat = catFactory.createAnimal();
        cat.makeSound();
    }
}
```

### 장점

- 객체 생성의 중앙 집중화: 객체 생성 로직을 한 곳에 모아 관리할 수 있음
- 유연성: 클라이언트 코드는 구체적인 클래스를 몰라도 되므로 객체 생성 로직의 변경이나 확장에 용이
- 코드 중복 감소: 동일한 객체 생성 코드를 여러 곳에 중복해서 사용하지 않고 팩토리 메소드를 통해 중복 제거 가능

### 단점

- 클래스 증가
- 복잡성 증가: 팩토리 패턴을 오버 엔지니어링할 경우 코드 복잡성 증가

## 옵저버 패턴(Observer Pattern)

객체 간 일대다 의존 관계를 정의, 어떤 객체의 상태가 변할 때 그 객체에 의존하는 다른 객체들이 자동으로 알림을 받고 업데이트 될 수 있도록 구성

객체 간 느슨한 결합을 가능하게 하며 이벤트 기반 시스템에서 많이 활용

### 구성 요소

- Subject(주체): 상태가 변경되는 주체 객체, 상태 관리와 옵저버들을 등록하고 알림을 보내는 메소드 제공
- Observer: 주체 객체의 상태 변화를 관찰하고 반응, 주체에서 발생한 변화에 대한 알림을 받아 적절한 동작 수행
- ConcreteSubject(구체적 주체): Subject 인터페이스를 구현하며 옵저버들을 등록하고 상태 변화를 알리는 메서드 구현
- ConcreteObserver(구체적 옵저버): Observer 인터페이스를 구현하며 주체 객체의 상태 변화에 따라 특정 동작을 수행

```jsx
// Subject 인터페이스
public interface Subject {
    void registerObserver(Observer observer);
    void removeObserver(Observer observer);
    void notifyObservers();
}

// Observer 인터페이스
public interface Observer {
    void update();
}

// 구체적인 주체 클래스
public class WeatherStation implements Subject {
    private List<Observer> observers;
    private int temperature;

    public WeatherStation() {
        observers = new ArrayList<>();
    }

    @Override
    public void registerObserver(Observer observer) {
        observers.add(observer);
    }

    @Override
    public void removeObserver(Observer observer) {
        observers.remove(observer);
    }

    @Override
    public void notifyObservers() {
        for (Observer observer : observers) {
            observer.update();
        }
    }

    public int getTemperature() {
        return temperature;
    }

    public void setTemperature(int temperature) {
        this.temperature = temperature;
        notifyObservers(); // 상태 변경 시 옵저버들에게 알림
    }
}

// 구체적인 옵저버 클래스
public class TemperatureDisplay implements Observer {
    private WeatherStation weatherStation;

    public TemperatureDisplay(WeatherStation weatherStation) {
        this.weatherStation = weatherStation;
        weatherStation.registerObserver(this);
    }

    @Override
    public void update() {
        System.out.println(weatherStation.getTemperature() + "도");
    }
}

// Client 클래스
public class Client {
    public static void main(String[] args) {
        WeatherStation weatherStation = new WeatherStation();
        TemperatureDisplay display1 = new TemperatureDisplay(weatherStation);
        TemperatureDisplay display2 = new TemperatureDisplay(weatherStation);

        // 온도가 변할 때마다 옵저버들에게 알림
        weatherStation.setTemperature(25); // 출력: "온도 디스플레이: 25도" (두 번 출력)
        weatherStation.setTemperature(30); // 출력: "온도 디스플레이: 30도" (두 번 출력)
    }
}
```

### 장점

- 느슨한 결합: 주체 객체와 옵저버 객체 간 느슨한 결합으로 의존성이 줄어듦
- 변화 관리: 상태 변화를 관리하고 다수의 객체들이 자동으로 업데이트 가능
- 확장성: 옵저버 추가, 제거에 용이

### 단점

- 너무 많은 알림: 옵저버나 업데이트가 많을 경우 불필요한 알림 발생
- 순서의 의존성: 옵저버들의 처리 순서가 중요한 경우에는 따로 관리

## 전략 패턴

객체의 행위를 클래스로 캡슐화하고 필요에 따라 행위를 교체

특정 알고리즘의 집합을 정의하고 각각을 캡슐화하여 이들을 교환할 수 있게 함

### 구성 요소

- 전략: 인터페이스나 추상 클래스로 특정 행위 정의
- 구체적인 전략: 전략 인터페이스를 구현한 실제 알고리즘 클래스
- 컨텍스트: 전략 객체를 사용하는 클라이언트, 전략을 실행하는 메서드를 호출하여 전략을 교체하거나 실행

```jsx
// PaymentStrategy 인터페이스
public interface PaymentStrategy {
    void pay(int amount);
}

// 신용카드 결제 전략
public class CreditCardPaymentStrategy implements PaymentStrategy {
    private String cardNumber;
    private String expiryDate;
    private String cvv;

    public CreditCardPaymentStrategy(String cardNumber, String expiryDate, String cvv) {
        this.cardNumber = cardNumber;
        this.expiryDate = expiryDate;
        this.cvv = cvv;
    }

    @Override
    public void pay(int amount) {
        System.out.println(amount + "원을 신용카드로 결제합니다.");
        // 신용카드 결제 처리 로직
    }
}

// 페이팔 결제 전략
public class PayPalPaymentStrategy implements PaymentStrategy {
    private String email;
    private String password;

    public PayPalPaymentStrategy(String email, String password) {
        this.email = email;
        this.password = password;
    }

    @Override
    public void pay(int amount) {
        System.out.println(amount + "원을 PayPal로 결제합니다.");
        // PayPal 결제 처리 로직
    }
}

// 결제를 처리하는 컨텍스트 클래스
public class PaymentContext {
    private PaymentStrategy paymentStrategy;

    public void setPaymentStrategy(PaymentStrategy paymentStrategy) {
        this.paymentStrategy = paymentStrategy;
    }

    public void executePayment(int amount) {
        paymentStrategy.pay(amount);
    }
}

// Client 클래스
public class Client {
    public static void main(String[] args) {
        PaymentContext paymentContext = new PaymentContext();

        // 신용카드로 결제
        PaymentStrategy creditCardStrategy = new CreditCardPaymentStrategy("1234 5678 9012 3456", "12/23", "123");
        paymentContext.setPaymentStrategy(creditCardStrategy);
        paymentContext.executePayment(10000);

        // PayPal로 결제
        PaymentStrategy paypalStrategy = new PayPalPaymentStrategy("example@example.com", "password123");
        paymentContext.setPaymentStrategy(paypalStrategy);
        paymentContext.executePayment(5000);
    }
}
```

### 장점

- 유연성과 확장성: 동일한 인터페이스를 사용하여 다양한 전략 적용 가능
- 코드 재사용: 전략은 독립적으로 캡슐화되어 재사용 가능
- 알고리즘 독립성: 알고리즘이 컨텍스트와 분리되어 있어 알고리즘의 변경이 컨텍스트에 영향을 주지 않음

### 단점

- 클라이언트가 전략을 명시적으로 설정해야함
- 컨텍스트와 전략 객체 간 복잡성

## 의존성 주입 패턴(Dependency Injection Pattern)

객체 간 의존 관계를 외부에서 설정

객체는 직접 필요한 의존 객체를 생성하거나 결정하지 않고 외부에서 주입받아 사용 가능

객체 간 결합도를 낮추고 유연성을 높임

### 주요 개념

- 의존성: 한 객체가 다른 객체를 사용할 때의 관계
- 의존성 주입: 외부에서 객체의 의존성을 설정하거나 주입, 주로 생성자 주입, setter 주입, 인터페이스 주입 등이 사용
- 주입 컨테이너: 의존성을 관리하고 주입하는 역할을 수행하는 프레임워크나 라이브러리(Spring Framework의 ApplicationContext 등)

```jsx
// 서비스 인터페이스
public interface MessageService {
    void sendMessage(String message);
}

// 구현 클래스
public class EmailService implements MessageService {
    @Override
    public void sendMessage(String message) {
        System.out.println("이메일을 보냅니다: " + message);
    }
}

// 의존성 주입을 받는 클라이언트 클래스
public class MyApplication {
    private final MessageService messageService;

    // 생성자 주입
    public MyApplication(MessageService messageService) {
        this.messageService = messageService;
    }

    public void sendNotification(String message) {
        messageService.sendMessage(message);
    }
}

// 클라이언트 코드
public class Client {
    public static void main(String[] args) {
        // 의존성 주입을 통해 EmailService 객체를 MyApplication에 주입
        MessageService emailService = new EmailService();
        MyApplication app = new MyApplication(emailService);
        app.sendNotification("안녕하세요!");
    }
}

// MyApplication 클래스 수정
public class MyApplication {
    private MessageService messageService;

    // setter 주입
    public void setMessageService(MessageService messageService) {
        this.messageService = messageService;
    }

    public void sendNotification(String message) {
        messageService.sendMessage(message);
    }
}

// 클라이언트 코드 수정
public class Client {
    public static void main(String[] args) {
        MessageService emailService = new EmailService();
        MyApplication app = new MyApplication();
        app.setMessageService(emailService);
        app.sendNotification("안녕하세요!");
    }
}
```

### 장점

- 유연성과 재사용성: 객체 간 결합도가 낮음
- 테스트 용이성: 의존성을 Mock 객체로 쉽게 대체 가능
- 관리 용이성: 주입된 객체의 라이프사이클 관리를 주입 컨테이너에 위임 가능

### 단점

- 복잡성
- 초기 설정 오류 발생 가능

## 어댑터 패턴

호환되지 않는 인터페이스를 함께 동작할 수 있도록 변환하는 구조적 패턴

주로 기존 클래스나 라이브러리를 수정없이 다른 인터페이스에 맞춰 사용해야할 때 사용

### 목적

기존 클래스나 라이브러리와 호환되지 않는 인터페이스를 가진 객체를 사용할 수 있도록 중간에 어댑터를 두어 인터페이스 변환

어댑터로 호환되지 않는 객체를 호환하고 코드의 유연성과 재사용성 증대

```jsx
// 기존에 제공되는 서비스
public interface LegacyService {
    void performAction();
}

public class LegacyServiceImpl implements LegacyService {
    @Override
    public void performAction() {
        System.out.println("Legacy service performing action...");
    }
}

// 새로운 인터페이스 정의
public interface NewService {
    void execute();
}

// 어댑터 클래스 구현
public class LegacyServiceAdapter implements NewService {
    private LegacyService legacyService;

    public LegacyServiceAdapter(LegacyService legacyService) {
        this.legacyService = legacyService;
    }

    @Override
    public void execute() {
        legacyService.performAction();
    }
}

// 클라이언트 코드
public class Client {
    public static void main(String[] args) {
        LegacyService legacyService = new LegacyServiceImpl();
        NewService newService = new LegacyServiceAdapter(legacyService);

        // 클라이언트는 NewService 인터페이스를 통해 기존의 LegacyService를 사용할 수 있음
        newService.execute();
    }
}
```

### 장점

- 호환성 확보: 기존 코드나 서드 파티 라이브러리의 인터페이스를 수정하지 않고 새로운 코드에서 사용 가능
- 재사용성: 다양한 인터페이스를 가진 여러 객체를 어댑터 패턴을 통해 통합 가능
- 유연성: 시스템에 새로운 요구 사항이나 변경 사항이 발생해도 기존 코드를 수정하지 않을 수 있음

### 단점

- 성능: 추가 객체 생성과 메서드 호출로 인한 성능 저하 가능성
- 과도한 사용의 위험: 시스템 구조의 복잡성 증가 가능성

# 데이터베이스 상호작용 패턴

## ORM(Object-Relation Mapping)

객체 지향 프로그래밍 언어와 관계형 데이터베이스 간 데이터 변환을 자동화

객체를 데이터베이스의 테이블에 매핑하고 객체 간 관계를 유지하며 데이터 액세스를 추상화

## 객체-관계 매핑(Object-Relation Mapping)

객체 지향 프로그래밍에서는 객체 간 관계를 코드로 쉽게 표현할 수 있지만 관계형 데이터베이스는 테이블 형태로 데이터를 저장하고 관리하기 때문에 이 두 사이의 불일치를 해결하기 위해 객체를 테이블로 매핑하고 객체 간 관계를 테이블로 매핑

대표적인 ORM 도구로는 Hibernate(Java). Django ORM(Python), Sequelize(Node.js) 등

```jsx
// Java 클래스
@Entity
public class Post {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String title;
    private String content;

    @ManyToOne(fetch = FetchType.LAZY)
    @JoinColumn(name = "author_id")
    private Author author;
	  
   // Getters and Setters
}

// Java 클래스
@Entity
public class Author {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    @OneToMany(mappedBy = "author", cascade = CascadeType.ALL, orphanRemoval = true)
    private List<Post> posts = new ArrayList<>();
        
    // Getters and Setters
}
```

### 장점

- 개발 생산성 향상
- 코드 가독성과 유지보수성 향상
- 데이터베이스 종속성 감소: 특정 데이터베이스 시스템에 종속되지 않음

### 단점

- 학습 곡선
- 성능 저하: 복잡한 쿼리나 대용량 데이터 처리 시 ORM의 추상화로 인한 성능 저하 발생 가능
- 추가 설정 필요

## Repository 패턴

데이터 액세스 로직을 캡슐화하여 도메인 객체와 데이터베이스를 분리

특히 데이터베이스와의 상호작용을 추상화하고 도메인 로직에서 데이터 액세스 코드를 분리하여 코드 유지보수성과 테스트 용이성 개선

### 구성 요소

- Entity: 데이터베이스의 테이블에 매핑되는 도메인 객체
- Repository Interface: 도메인 객체를 CRUD하기 위한 메서드를 정의하는 인터페이스
- Concrete Repository: Repository Interface를 구현

```jsx
// Repository Interface
public interface ProductRepository {
    Product findById(Long id);
    List<Product> findAll();
    void save(Product product);
    void update(Product product);
    void delete(Product product);
}

// Concrete Repository
public class JpaProductRepository implements ProductRepository {
    private EntityManager entityManager;

    public JpaProductRepository(EntityManager entityManager) {
        this.entityManager = entityManager;
    }

    @Override
    public Product findById(Long id) {
        return entityManager.find(Product.class, id);
    }

    @Override
    public void save(Product product) {
        entityManager.persist(product);
    }

    @Override
    public void update(Product product) {
        entityManager.merge(product);
    }

    @Override
    public void delete(Product product) {
        entityManager.remove(product);
    }
}
```

### 장점

- 데이터베이스 추상화: 도메인 로직은 Repository를 통해 데이터베이스와 직접적으로 상호작용하지 않고 Repository가 데이터 액세스를 관리
- 유지보수성 향상
- 단위 테스트 용이성: Repository 인터페이스를 Mock 객체로 대체하여 단위 테스트 수행 가능

### 단점

- 추가적인 코드 복잡성
- 학습 곡선

## CQRS(Command Query Responsivility Segregation)

명령(Command)과 조회(Query)를 분리하여 처리

데이터 수정과 조회를 서로 다른 모델로 처리함으로써 성능, 확장성, 유지보수성 개선

### 구성 요소

- Command: 데이터 변경 목적으로 하는 요청, 데이터베이스의 상태를 변경, 주로 비동기적으로 처리
- Query: 데이터 조회 목적으로 하는 요청, 읽기 전용 데이터 반환, 빠른 응답과 함께 최적화된 형태로 처리
- Command Model: 데이터 수정을 위한 모델, 주로 업데이트 지향 데이터 모델로 구현
- Query Model: 데이터 조회를 위한 모델, 주로 읽기 최적화된 데이터 모델로 구현

```jsx
// Command 모델 예시
public class CreateOrderCommand {
    private String customerId;
    private List<String> productIds;

// Constructor, getters, setters
}

// Command Handler 예시
@Service
public class OrderCommandHandler {
    @Autowired
    private OrderRepository orderRepository;

    @Transactional
    public void handle(CreateOrderCommand command) {
        Order order = new Order(command.getCustomerId(), command.getProductIds());
        orderRepository.save(order);
    }
}

// Query 모델 예시
@Entity
public class OrderView {
    @Id
    private String orderId;
    private String customerId;
    private List<String> productIds;

    // Constructors, getters, setters
   
}

// Query Handler 예시
@Service
public class OrderQueryHandler {
    @Autowired
    private EntityManager entityManager;

    public OrderView getOrder(String orderId) {
        return entityManager.find(OrderView.class, orderId);
    }

    public List<OrderView> getAllOrders() {
        return entityManager.createQuery("SELECT o FROM OrderView o", OrderView.class).getResultList();
    }
}
```

### 장점

- 성능 향상: 읽기, 쓰기를 분리함으로 각각의 작업에 최적화된 데이터 모뎅 사용 가능
- 확장성: 읽기와 쓰기 작업을 독립적으로 확장 가능, 각각에 맞는 리소스를 최적화하여 시스템 전체적인 확장성을 높임
- 유지보수성

### 단점

- 복잡성: 두 개의 모델을 유지해야하므로 초기 구현이나 복잡한 비즈니스 요구사항에 대응하기 위한 추가적 노력 필요
- 학습 곡선
