# 시큐리티 코딩

시큐리티 코딩은 보안 취약점을 방지하고 악의적인 공격으로부터 시슽쳄을 보호하기 위한 코딩 기법과 원칙

사전 예방적 접근을 통해 코드가 예상치 못한 상황에서도 안전하게 동작하도록 보장하는 것이 중요

## 중요성 및 필요성

민감한 사용자 정보 및 기업 데이터를 보호하고 데이터 유출 및 손실을 방지하는데 필수적

보안 취약점으로 인해 시스템이 장애를 겪거나 손상되지 않도록 하여 서비스 가용성과 신뢰성 확보 가능

## 정보 보안 규정 및 표준

### GDPR (General Data Protection Regulation)

유럽 연합 내 모든 개인 데이터 보호 및 프라이버시를 강화하고 통일하기 위해 제정된 법규

데이터 주체의 권리(접근권, 수정권, 삭제권 등), 데이터 처리 원칙, 데이터 보호 책임자의 역할, 데이터 유출 시 통보 의무 등을 포함

### CCPA (Califonia Consumer Privacy Act)

캘리포니아에 거주하는 소비자들의 개인 정보 보호를 강화하고 데이터 주체의 권리를 보장하기 위해 제정된 법규

소비자의 접근권, 삭제권, 데이터 판매 거부권, 편등 서비스 및 가격 제공권을 포함하며 기업은 개인정보 보호 정책공개와 소비자 요청 처리 등의 의무를 가짐

### ISMS (Information Security Management System)

정보의 기밀성, 무결성, 가용성을 보장하기 위해 정보 보안 관리 체계를 수립하고 유지하는 국제 표준

기업의 정보 보호 관리 체계에 대한 인증 제도

정보 보안 정책 수립, 위험 평가 및 관리, 보안 통제 조치, 지속적인 모니터링 및 개선을 포함

인증은 ISO/IEC 27001 표준에 따라 수행

### 개인정보 보호법 (Personal Information Protection Act, PIPA)

대한민국 내 개인 정보를 보호하고 개인정보 처리에 대한 권리를 보장하기 위해 제정된 법규

개인정보 수집 및 이용 동의, 정보 주체 접근권 및 삭제권, 개인 정보 보호 조치 의무, 개인정보 유출 시 통보 의무를 포함

## 시큐리티 코딩 기본 원칙

### 1. 입력 데이터 검증

- 모든 입력 데이터를 검증하여 악의적인 입력 방지
- 화이트리스트 방식을 사용하여 유효한 입력만 허용하고 정규 표현식을 통해 입력 형식을 검증

### 2. 출력 데이터 인코딩

- 출력 데이터를 적절히 인코딩하여 XSS 등의 공격 방지
- HTML, JavaScript, SQL 등 각 맥락에 맞는 인코딩 적용

### 3. 암호화

- 중요 데이터를 암호화하고 안전하게 저장해야 함
- 전송 중 데이터는 SSL/TLS를 통해 암호화하고 민감 데이터에 접근 시 로그를 기록

### 4. 접근 권한 제어

- 최소 권한 원칙을 준수하여 불필요한 접근을 제한
- 역할 기반 접근 제어(RBAC)를 적용하고 세션 관리 및 강력한 인증 메커니즘을 사용

### 5. 제한된 정보 제공

- 에러 메시지에 민감한 정보 미포함
- 일반 사용자에게 구체적인 에러 정보를 노출하지 않으며 보안 이벤트 및 접근 시도에 대한 상세한 로깅 실시
- 로그 파일의 무결성을 유지하고 접근을 제어

# 보안 사고 사례 분석

## Polifill.js 공급망 공격

### 공급망 공격이란?

- 공격자가 소프트웨어나 하드웨어의 공급망을 침해하여 사용자가 사용하는 제품에 악성 코드를 삽입하거나 취약점을 추가하는 사이버 공격
- 공격자는 주로 소프트웨어 업데이터, 제 3자 공급업체, 또는 하드웨어 구성 요소를 통해 공격 수행

### Polyfill.js 사례

- Polyfill.js는 오래된 브라우저 지원을 위한 오픈 소스 라이브러리로 10만개 이상의 사이트에서 사용 중
- 올해 2월 중국 회사가 Polyfill.js의 도메인과 Github 계정을 인수한 수 해당 도메인을 통해 모바일 기기에 악성코드를 주입하기 시작

### 공격 사례

- 공격 방식: HTTP 헤더를 기반으로 동적 생성된 코드가 특정 모바일 기기에서 특정 시간에만 활성화되며 관리자 사용자나 웹 분석 서비스가 감지되면 실행을 지연
- 악성코드 예시: 모바일 사용자를 가짜 구글 애널리틱스 도메인을 통해 스포츠 베팅 사이트로 리디렉션
- 대응 방안: Polyfill.js의 원저자는 현대 브라우저에서는 더 이상 필요하지 않으므로 더 이상 라이브러리를 사용하지 말 것을 권장하며 Fastly, Cloudflare가 신뢰할 수 있는 대안을 제공
- 이 사건은 전형적인 공급망 공격 사례

### 에방

- 공급망 보안 검토와 모니터링, 공급업체와 보안 협력 강화
- 정기적인 보안 감사
- 소프트웨어 업데이트 및 패치 검증

### 대응

- 공격 즉시 유출된 데이터의 범위와 피해 파악
- 침해된 시스템 격리 및 복구, 추가 공격 방지를 위한 보안 조치 강화
- 공격에 대한 정보 공유

## Twilio Authy 사용자 데이터 유출

해커가 Twilio의 인증 앱 Authy의 사용자 데이터베이스를 침해하여 약 3300만 명의 전화번호 유출

유출된 전화번호는 인증 및 보안 서비스에 사용되며 해커는 이를 통해 스팸, 피싱 공격, 사용자 계정 탈취 등 다양한 악용 가능

인증 시스템과 내부 보안 조치의 취약점을 악용하여 대량의 전화번호 데이터를 뺴내는데 성공

### 예방

- 인증 시스템과 네트워크 보안 강화, 정기적 보안 점검과 취약점 평가 수행
- 엄격한 접근 권한 관리, 최소 권한 원칙 적용
- 실시간 보안 모니터링과 침입 탐지 시스템

### 대응

- 사고 조사 및 원인 분석
- 피해자 통보
- 보안 조치 강화

# 시큐리티 코딩 베스트 프랙티스

## 입력 데이터 검증

- 화이트 리스트 검증: 허용된 데이터 형식과 값을 정의하고 입력 데이터가 기준에 맞는지 확인
- 길이 제한: 입력 필드의 최대 길이를 제한하여 버퍼 오버플로우 공격 방지
- 특수 문자 필터링: SQL 삽입 및 XSS 공격을 방지하기 위해 특수 문자 필터링, 이스케이프

### XSS (Cross-Site Scripting)

XSS는 곡격자가 악의적인 스크립트를 웹페이지에 삽입하여 사용자 브라우저에서 실행되도록 하는 사이버 공격

주로 자바스크립트를 사용하며 공격자가 사용자 정보를 탈취하거나 악성코드를 배포하는데 사용

## 데이터 인코딩

- 웹 앱에서 사용자에게 표시되는 데이터를 안전하게 변환
- HTML 인코딩: HTML 콘텐츠에 특수 문자를 HTML 엔티티로 변환하여 XSS 공격 방지
- URL 인코딩: URL에 포함되는 데이터는 URL 인코딩하여 쿼리 문자열 및 경로를 안전하게 처리
- 문자열 인코딩: 데이터베이스에서 반환되는 문자열을 인코딩하여 SQL 인젝션 공격 방지

### SQL Injection

공격자가 악의적인 SQL 코드를 앱 입력 필드에 삽입하여 데이터베이스 쿼리를 조작하는 공격

데이터베이스 정보를 조회하거나 수정, 삭제할 수 있으며 데이터베이스 서버에 대한 권한을 얻을 수 있음

## 데이터 보호

- 데이터의 기밀성, 무결성 및 가용성 유지를 위한 조치를 취함
- 암호화: 저장 데이터와 전송 데이터를 암호화하여 무단 접근과 데이터 유출 방지
- 접근 제어: 데이터 접근 권한을 관리하고 필요한 권한만 부여
- 백업: 정기적 데이터 백업을 통해 데이터 손실에 대비

## 암호화 및 해싱

암호호는 데이터를 변형하여 기밀성을 유지하고 해싱은 데이터의 무결성을 확인하는데 사용

### 암호화

- 대칭 암호화: 동일한 키를 사용하여 데이터를 암호화하고 복호화
    - AES, DES
- 비대칭 암호화: 공개키와 비공개키를 사용하여 데이터를 암호화하고 복호화
    - RSA, ECC

### 해싱

- 해시 알고리즘: 데이터 무결성 보장을 위해 SHA-256, SHA-3 등의 강력한 해시 알고리즘 사용
- 솔팅: 해시 값에 임의의 데이터를 추가하여 동일한 입력값에 대해 다른 해시 값을 생성

## 인증 및 권한 부여

사용자 및 시스템 신원 확인 및 접근 제어

- 강력한 인증: 다단계 인증(MFA) 및 강력한 암호 정책을 사용하여 사용자 인증 강화
- 권한 최소화: 사용자가 필요로 하는 최소한의 권한만 부여
- 세션 관리: 세션 타임아웃 및 재인증 절차를 구현하여 세션 하이재킹 방지

## 에러 및 로깅 관리

- 시스템 오류 및 이벤트 기록를 기록하고 보안 위협에 대한 분석과 문제 해결 지원
- 에러 메시지: 상세 오류 메시지와 시스템 내부 정보를 사용자에게 노출하지 않음
- 로깅: 중요 보안 이벤트와 시스템 활동을 기록하여 사건 발생시 분석과 대응을 용이하게 함
- 로그 보호: 로그 파일에 대한 접근 제어 강화, 로그 데이터의 무결성 보호
- 모니터링: 로그를 실시간으로 모니터링하여 이상 징후 조기 탐지 및 대응

# 웹 앱 시큐리티

## OWASP Top 10

OWASP(Open Web Application Security Project) Top 10은 웹 앱에서 가장 심각한 보안 취약점 10가지를 매년 발표하는 목록

웹 앱의 보안을 강화하고 보안 취약점을 사전에 식별하여 대응할 수 있도록 하는 것이 목표

최신 버전은 OWASP Top 10-2024이며 매년 업데이트

## A01- 접근 제어 취약점 (Broken Access Control)

사용자가 허가되지 않은 자원에 접근할 수 있는 취약점

인증되지 않은 액세스나 권한 상승 문제 포함

### 대응 방안

- 사용자에게 최소 권한만 부여
- 모든 요청에 대해 서버 측에서 권한 검증
- 사용자 권한을 정기적으로 검토하고 조정
- 사용자가 잘못된 권한을 획득하지 않도록 인증 보안 강화

```java
// 권한 검증 X
@GetMapping("/user/{id}")
public ResponseEntity<User> getUser(@PathVariable Long id) {
    User user = userService.findById(id);
    return ResponseEntity.ok(user);
}

// 권한 검증
@GetMapping("/user/{id}")
public ResponseEntity<User> getUser(@PathVariable Long id) {
    if (!securityService.hasAccessToUser(id)) {
        return ResponseEntity.status(HttpStatus.FORBIDDEN).build();
    }
    User user = userService.findById(id);
    return ResponseEntity.ok(user);
}
```

## A02 - 암호화 실패(Cryptographic Failures)

암호화 불완전성이나 취약한 암호화 알고리즘 사용으로 발생하는 문제

### 대응 방안

- AES-256, RSA 등의 강력한 최신 암호화 알고리즘 사용
- 암호화 키가 유출되지 않도록 키를 안전하게 저장하고 관리
- 암호화 방법과 키 관리 절차를 정기적으로 검토

```java
// 취약한 DES 사용
public class EncryptionExample {
    public static void main(String[] args) throws Exception {
        SecretKey key = KeyGenerator.getInstance("DES").generateKey();  // 취약한 DES 사용
        Cipher cipher = Cipher.getInstance("DES/ECB/PKCS5Padding");
        cipher.init(Cipher.ENCRYPT_MODE, key);
        byte[] encrypted = cipher.doFinal("data".getBytes());
        System.out.println(new String(encrypted));
    }
}

// 안전한 AES 사용
public class EncryptionExample {
    public static void main(String[] args) throws Exception {
        SecretKey key = KeyGenerator.getInstance("AES").generateKey();  // 안전한 AES 사용
        Cipher cipher = Cipher.getInstance("AES/CBC/PKCS5Padding");
        IvParameterSpec iv = new IvParameterSpec(new byte[16]);  // 초기화 벡터
        cipher.init(Cipher.ENCRYPT_MODE, key, iv);
        byte[] encrypted = cipher.doFinal("data".getBytes());
        System.out.println(new String(encrypted));
    }
}
```

## A03 - 인젝션

악의적 입력이 쿼리나 명령어에 삽입되어 시스템을 조작하는 공격

SQL, NoSQL, OS 명령어 인젝션 등이 포함

### 대응 방안

- 매개변수화된 쿼리와 준비된 문장을 사용하여 SQL 인젝션 방지
    - 사용자 입력 데이터를 가공하지 않고 직접 사용하지 않음
- 모든 사용자 입력 검증 후 유효 데이터만 처리
- 데이터베이스 오류 메시지를 사용자에게 노출하지 않음
    - 내부 시스템 구조와 보안 취약점이 노출되지 않도록 함

```java
// 취약한 쿼리 사용
@GetMapping("/user")
public ResponseEntity<User> getUserByUsername(@RequestParam String username) {
    String query = "SELECT * FROM users WHERE username = '" + username + "'";  // 취약한 쿼리 실행
    User user = jdbcTemplate.queryForObject(query, new UserRowMapper());
    return ResponseEntity.ok(user);
}

// 보안이 강화된 쿼리 사용
@GetMapping("/user")
public ResponseEntity<User> getUserByUsername(@RequestParam String username) {
    String query = "SELECT * FROM users WHERE username = ?";  // 매개변수화된 쿼리 사용
    User user = jdbcTemplate.queryForObject(query, new Object[]{username}, new UserRowMapper());
    return ResponseEntity.ok(user);
}
```

## A04 - 안전하지 않은 설계(Insecure Design)

- 설계 단계에서 보안이 고려되지 않은 경우 발생하는 취약점

### 대응 방안

- 설계 단계에서 보안 요구 사항을 명확히 정의하고 적용
- 앱 위협 모델을 분석하고 설계에 반영
- 설계 단계에서 보안 검토와 테스트 수행

## A05 - 보안 설정 오류(Security Misconfiguration)

시스템이나 앱 보안 설정이 잘못되어 취약점 발생

### 대응 방안

- 시스템과 앱 보안 설정을 정기적으로 검토하고 조정
- 자동화 도구를 사용하여 보안 설정 일관성 유지
- 기본 보안 설정 변경으로 보안 강화

```java
// 디버그 로깅 활성화
@Configuration
public class WebConfig implements WebMvcConfigurer {
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        registry.addInterceptor(new LoggingInterceptor());  // 디버그 로깅 활성화
    }
}

// 개발 환경에서만 활성화
@Configuration
public class WebConfig implements WebMvcConfigurer {
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        if (!"production".equals(System.getProperty("env"))) {
            registry.addInterceptor(new LoggingInterceptor());  // 개발 환경에서만 활성화
        }
    }
}
```

## A06 - 취약하고 오래된 컴포넌트(Vulnerable and Outdated Components)

취약점이 있는 오래된 소프트웨어 구성 요소 사용

### 대응 방안

- 사용 라이브러리와 소프트웨어의 최신 버전을 유지
- 공개된 취약점 데이터베이스를 모니터링하고, 취약점 발견시 신속히 대응
- 최신 보안 패치 적용

## A07 - 식별 및 인증 실패(Identification and Authentication Failures)

사용자 인증 및 식별 관련 취약점으로 비밀번호 우회, 인증 토큰 탈취 등이 포함

### 대응 방안

- 강력한 인증 방법을 사용하여 인증 보안 강화
- 강력한 비밀번호 정책을 적용하고 정기적 비밀번호 변경 권장
- 세션 타임아웃 및 세션 무효화 절차 구현

```java
// 비밀번호를 평문으로 저장
@PostMapping("/register")
public ResponseEntity<String> registerUser(@RequestParam String password) throws IOException {
    Files.write(Paths.get("passwords.txt"), password.getBytes());  // 비밀번호를 평문으로 저장
    return ResponseEntity.ok("User registered");
}

// 비밀번호를 해싱하여 저장
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;

@PostMapping("/register")
public ResponseEntity<String> registerUser(@RequestParam String password) throws IOException {
    BCryptPasswordEncoder encoder = new BCryptPasswordEncoder();
    String hashedPassword = encoder.encode(password);  // 비밀번호를 해싱하여 저장
    Files.write(Paths.get("passwords.txt"), hashedPassword.getBytes());
    return ResponseEntity.ok("User registered");
}
```

## A08 - 소프트웨어 및 데이터 무결성 실패

소프트웨어와 데이터의 무결성 관련 취약점으로, 데이터 변조나 무결성 검증 부족이 포함

안전하지 않은 CI/CD 파이프라인은 개발 및 배포 과정에서 애플리케이션이 변조되면 무결성이 훼손될 가능성이 있으므로, 애플리케이션이 사용하는 코드에 대한 무결성 검증 절차를 추가해야 함

### **대응 방안**

- 데이터와 소프트웨어의 무결성을 검증하는 메커니즘을 사용
- 소프트웨어와 데이터에 디지털 서명을 적용하여 무결성을 보장
- 코드에 대한 무결성 검토를 정기적으로 수행

## **A09 - 보안 로깅 및 모니터링 실패 (Security Logging and Monitoring Failures)**

보안 로그와 모니터링의 부족으로, 보안 사건을 적시에 탐지하고 대응하지 못하는 경우

### **대응 방안**

- 중요한 보안 이벤트를 기록하고, 로그를 안전하게 저장
- 보안 이벤트를 실시간으로 모니터링하고 이상 징후를 탐지
- 정기적으로 로그를 분석하여 보안 사건을 식별

```java
@PostMapping("/login")
public ResponseEntity<String> login(@RequestParam String username, @RequestParam String password) {
    // 로그인 인증 로직
    return ResponseEntity.ok("Logged in");
}

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

@PostMapping("/login")
public ResponseEntity<String> login(@RequestParam String username, @RequestParam String password) {
    Logger logger = LoggerFactory.getLogger(this.getClass());
    logger.info("Login attempt for username: {}", username);
    // 로그인 인증 로직
    return ResponseEntity.ok("Logged in");
}
```

## **A10 - 서버 사이드 요청 위조 (Server-Side Request Forgery / SSRF)**

공격자가 서버 측에서 요청을 보내도록 조작하여 내부 시스템에 접근하거나 외부 리소스를 수집하는 공격

### **대응 방안**

•	사용자 입력을 철저히 검증하고, 외부 요청을 제한

•	서버의 네트워크 접근을 제어하여 내부 자원에 대한 무단 접근을 방지

•	서버가 접근할 수 있는 리소스를 최소화하여 피해를 줄임

# 시큐어 코딩 도구 및 프레임워크

## 정적 분석 도구

코드가 실행되기 전 소스 코드나 바이트 코드를 분석하여 보안 취약점이나 코드 품질 문제를 식별하는 도구

### 기능

- 소스 코드 내 잠재적인 보안 취약점 탐지
- 코드 문법 오류 및 논리적 결함 발견
- 보안 코딩 표준 및 규정 준수 확인

### 예시 도구

- SonarQube: 코드 품질 및 보안 분석 후 취약점 보고
- Checkmarx: 정적 분석을 통해 보안 취약점을 찾아내고 코드 개선 제안
- Fortify Static Code Analyzer: 보안 결함을 발견하고 개선 권장 사항 제공

## 동적 분석 도구

앱이 실행 중일 때 동작을 분석하여 보안 취약점, 성능 문제, 다른 결함을 식별하는 도구

### 기능

- 앱의 런타임 동작을 분석하여 취약점 탐지
- 실제 공격 시나리오를 기반으로 취약점 식별
- 앱 성능 문제를 발견하고 개선

### 예시 도구

- OWASP ZAP(Zed Attack Proxy): 웹 앱의 보안 취약점 발견 도구
- Burp Suite: 웹 앱의 보안 테스트와 취약점 분석
- Betsparker: 웹 앱의 보안 취약점 자동 탐지

## 보안 프레임워크 및 라이브러리

보안 기능과 모범 사례를 구현하는 데 도움이 되는 개발 프레임워크와 라이브러리

보안 기능을 신속히 적용하고 표준을 준수하도록 도와줌

### 기능

- 인증, 권한 부여, 암호화 등 보안 기능 포함
- 코딩 표준 준수: 보안 코딩 표준을 준수할 수 있도록 도움
- 보안 결함 방지: 취약점 발생 가능성을 줄임

### 예시 프레임워크 및 라이브러리

- Spring Security: Java 기반의 앱에서 인증, 권한 부여 및 보안 관리 제공
- OWASP ESAPI(Enterprise Security API): 앱 보안을 강화하는 다양한 보안 기능 제공
- Helmet: Node.js 앱의 보안 강화를 위한 HTTP 헤더 설정 라이브러리

# DevSecOps 및 지속적인 보안 통합

## DevSecOps의 개념과 중요성

DevSecOps는 개발, 보안, 운영의 통합을 통해 소프트웨어 개발 주기 전반에 걸쳐 보안을 강화하는 접근 방식

### 중요성

- 개발 초기 단계에서 보안을 통합하여 취약점을 조기에 발견하고 수정 가능
- 보안 검토와 테스트가 자동화되어 배포 속도를 저하시키지 않으면서 안전성 보장
- 개발, 보안, 운영 팀 간 원활한 협업을 통해 보안 문제를 신속히 해결 가능
- 보안 업데이트와 패치를 자동화하여 지속적으로 시스템 보호 가능

### → CI/CD 파이프라인에 소프트웨어 보안 검증 프로세스를 추가하여 소프트웨어 개발 주기 전반에 걸쳐 보안 강화

## CI/CD 파이프라인에 보안 통합하기

### 방법

- 정적 분석 도구 통합: CI 파이프라인에 정적 분석 도구를 통합하여 코드가 커밋될 때마다 보안 취약점을 자동으로 분석
- 동적 분석 도구 통합: CD 파이프라인에 동적 분석 도구를 통합하여 배포된 앱의 런타임 보안 테스트 수행
- 보안 정책 적용: CI/CD 설정에 보안 정책을 적용하여 모든 빌드와 배포가 보안 기준을 만족하도록 보장
- 비밀 관리: CI/CD 파이프라인에서 민감한 정보를 안전하게 관리하고 전달하기 위한 비밀 관리 도구 사용

![image](https://github.com/user-attachments/assets/68d89601-eae5-4ac0-a027-fcdf2274d1a6)

## SBOM(Software Bill of Materials)

소프트웨어의 모든 구성 요소, 라이브러리, 의존성 및 해당 메타데이터를 기록한 목록

소프트웨어 구성 요소와 출처를 명확히 하고 보안 및 컴플라이언스 관리를 용이하게 함

### 중요성

- 사용 중인 라이브러리 및 의존성의 취약점을 빠르게 식별하고 대응할 수 있음
- 소프트웨어의 구성 요소가 사용하는 라이센스 규정을 준수하는지 검토할 수 있음
- 보안 사고 발생 시 소프트웨어 구성 요소를 분석하여 문제 범위를 파악하고 대응할 수 있음
- 소프트웨어 공급망의 투명성을 확보하여 신뢰성을 높일 수 있음

## CycloneDX와 SPDX

- CycloneDX: SBOM을 생성하고 관리하기 위한 오픈 소스 표준
- SPDX: 소프트웨어 라이센스 및 컴포넌트 정보를 문서화하는 표준
- 다양한 SBOM을 사용하여 소프트웨어 구성 요소에 대한 보고서를 작성하고 보안 및 라이센스 관련 문제를 명확히 전달 가능
- CI/CD 파이프라인에 SBOM 생성 및 검토 과정을 통합하여 이러한 내용을 자동화

![image](https://github.com/user-attachments/assets/acd9517f-c96d-45ef-bf1d-694e3618068c)

## CycloneDX

OWASP에서 개발한 오픈 소스 SBOM 형식으로 소프트웨어 공급망의 위험 식별과 취약점 관리를 목적으로 함

### 특징

- 정보 포맷: XML 및 JSON 포맷을 지원
- 자동화 지원: 소프트웨어 빌드 주기 전반에 걸쳐 SBOM 생성 자동화를 지원
- 취약점 식별: 구성 요소의 보안 취약점을 식별

### 주요 필드

- BOM 메타데이터: 소프트웨어 제조업체/공급업체 및 도구의 메타데이터
- 구성 요소: 소프트웨어의 모든 구성 요소에 대한 설명
- 서비스: 외부 API, 엔드포인트 URL 및 인증 요구 사항
- 종속성: 소프트웨어 구성 요소 간 직접적이고 전이적인 관계
- 확장: 향후 기능 확장을 위한 데이터 제공

### 사용 예시

- 취약점 관리 및 보안 모니터링
- 자동화된 SBOM 생성

## SPDX

Linux Foundation이 개발한 오픈 소스 프로젝트로 주로 소프트웨어 라이센스 관리와 규정 준수를 위해 설계됨

### **특징**

- **정보 포맷**: JSON, RDF, Tag/Value 포맷을 지원
- **라이센스 준수**: 소프트웨어의 라이센스 정보를 명확히 기록하여 법적 요구사항을 준
- **상호 운용성**: 다른 SBOM 형식과의 호환성을 높이기 위한 기능을 포함

### **주요 필드**

- **문서 생성 정보**: SBOM 문서의 생성일 및 처리 도구 정보
- **패키지 정보**: 소프트웨어 패키지와 관련된 정보
- **파일 정보**: 패키지에 포함된 파일의 이름, 라이센스, 저작권 정보
- **스니펫 정보**: 코드 조각이 다른 소스에서 가져온 경우
- **관계 및 주석**: 문서 내 구성 요소 간의 관계를 설명합니다.

### **사용 예시**

- 라이센스 준수 확인 및 소프트웨어 구성 요소에 대한 세부 정보 문서화

## CycloneDX와 SPDX 요약

- SPDX는 라이센스 관리 및 소프트웨어 패키지에 대한 투명한 정보를 제공하는 데 유용하며 소프트웨어 개발 및 규정 준수 관리에 적합
- CycloneDX는 보안 취약점 식별 및 소프트웨어 공급망의 투명성 확보를 중시하며 SBOM 생성을 자동화하고 관리하는데 효과적

![image](https://github.com/user-attachments/assets/3cad12b8-e683-4762-8cbd-3a094018abd4)

## 지속적인 모니터링 및 대응

- 시스템을 지속적으로 모니터링하고 보안 위협에 신속히 대응하는 프로세스

### 방법

- 앱 및 인프라 로그를 실시간으로 수집하고 분석하여 이상 징후를 조기 발견
- 네트워크 및 시스템의 비정상적인 활동을 탐지하고 경고
- 보안 이벤트 발생 시 자동 알림 발송 후 대응 절차 실행
- 보안 사고 발생 시 신속하게 대응할 수 있는 절차와 계획을 수립

## 보안 문화 구축 및 팀 협업

조직 내에서 보안을 중요시하고 모든 팀원들이 보안에 대한 책임을 공유하는 문화를 구축하는 과정

### 방법

- 개발자와 운영팀에게 정기적으로 보안 교육을 제공하여 보안 인식 제고
- 개발, 보안, 운영 팀 간의 원활한 협업을 통해 보안 문제 해결
- 보안 관련 정보를 팀에 공유하고 보안 문제 발생 시 협력하여 해결
- 보안 우수 사례를 문서화하고 팀 내에서 공유하여 모범 사례
