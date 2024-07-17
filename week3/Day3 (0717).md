# 인증

사용자나 시스템의 신원을 검증하는 것

## 인증 방법

- 기본 인증
- 토큰 기반 인증: 사용자 인증 후 서버가 토큰을 발급하며 이후 요청에서 토큰을 사용하는 방식(예. JWT 토큰)
- OAuth: 제 3자 앱이 사용자 자원에 접근할 수 있도록 허용하는 방식
- SSO: 한 번의 로그인으로 여러 앱에 접근할 수 있는 방식

### 기본 인증

사용자가 HTTP 헤더를 통해 사용자의 ID와 비밀번호를 전송하여 인증하는 방식

사용자 이름과 비밀번호가 Base64로 인코당되어 전송되며 암호화는 적용되지 않기 때문에 보안에 취약

사용자 ID: 비밀번호 → Base64 Encoding

하지만 HTTPS에서는 데이터가 SSL/TLS를 통해 암호화되어 보안이 강화

```java
public class BasicAuthFilter implements Filter {

    @Override
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) 
            throws IOException, ServletException {
        HttpServletRequest httpRequest = (HttpServletRequest) request;
        HttpServletResponse httpResponse = (HttpServletResponse) response;

        String authHeader = httpRequest.getHeader("Authorization");
        if (authHeader != null && authHeader.startsWith("Basic")) {
            String encodedCredentials = authHeader.substring("Basic".length()).trim();
            String decodedCredentials = new String(Base64.getDecoder().decode(encodedCredentials));
            String[] credentials = decodedCredentials.split(":", 2);

            if (credentials.length == 2 && isValidCredentials(credentials[0], credentials[1])) {
                chain.doFilter(request, response);
                return;
            }
        }

        unauthorized(httpResponse, "Unauthorized");
    }
  }

```

## 세션 기반 인증

![image](https://github.com/user-attachments/assets/9a7bded0-c9c6-457d-b183-afee5d5ac2f6)

사용자가 로그인하면 서버가 세션을 생성하고 클라이언트는 쿠키를 통해 세션 ID를 유지하는 방식

- 쿠키와 세션의 개념
    - 쿠키: 클라이언트 측에 저장되는 작은 데이터 파일로 사용자의 상태 정보를 유지, 쿠키에는 세션 ID와 같은 인증 정보가 포함될 수 있음
    - 세션: 서버 측에 저장되는 사용자 정보로 사용자 상태를 관리, 고유한 세션 ID로 식별
- 세션 관리 메커니즘
    - 사용자가 로그인하면 서버가 고유한 세션 ID를 생성하고 이를 클라이언트에 쿠키로 전송
    - 클라이언트는 이후 모든 요청에서 쿠키를 통해 세션 ID를 서버에 전송하여 인증 유지
    - 서버는 세션 ID를 통해 사용자 상태를 식별하고 관리
    - 세션은 서버 측에 저장되어 서버 자원을 많이 사용

```java
// 세션 생성 예시
public class SessionExampleServlet extends HttpServlet {

    protected void doGet(HttpServletRequest request, HttpServletResponse response) {
        HttpSession session = request.getSession(true); // 세션이 없으면 세션 생성
        String sessionId = session.getId(); // 세션 ID 가져오기
        response.getWriter().write("Session ID: " + sessionId);
    }
}
```

```jsx
const express = require("express");
const session = require("express-session");
const uuid = require("uuid");

const app = express();

// 세션 설정
app.use(
    session({
        secret: "your_secret_key",
        resave: false,
        saveUninitialized: true,
        genid: function (req) {
            return uuid.v4(); // UUID를 사용하여 세션 ID 생성할 수 있음
        },
    })
);
```

- 세션 ID는 중복되면 안됨

### 세션 기반 인증 시 서버에서 인증을 확인하는 방법

1. 세션 생성
    - 서버는 고유한 세션 ID 생성
    - 세션 ID는 사용자 정보를 포함한 세션 데이터와 함께 서버 메모리, 데이터베이스 또는 다른 저장소에 저장
2. 세션 ID를 클라이언트에 전달
    - 서버는 세션 ID를 클라이언트에 쿠키로 전달
    - 클라이언트는 세션 ID를 브라우저 쿠키에 저장
3. 서버에서 세션 ID 검증
    - 서버는 클라이언트 요청을 받을 때 요청에 포함된 세션 ID를 사용하여 서버에 저장된 세션 데이터와 비교
4. 인증 확인 및 사용자 정보 로드
    - 세션 ID가 유효하지 않다면 인증 실패 반환

### 장점

- 보안: 클라이언트에게 세션 ID만 전송하므로 중간자 공격에 강함
- 서버 부담 감소: 세션 ID만을 클라이언트에 전송하므로 서버에 저장된 세션 데이터를 통해 인증을 유지할 수 있어 서버 부하가 감소
- 탈취 방지: 세션 ID는 브라우저 쿠키에 저장되며 이는 XSS(Cross-Site Scripting)공격으로부터 보호

### 단점

- 상태 유지: 서버에 상태를 유지해야하므로 확장성이 떨어지고 서버에 부하
- 확장성: 서버의 스케일링이 어려울 수 있으며 서버 장애 시 세션 정보의 손실 발생 가능

## 토큰 기반 인증

![image](https://github.com/user-attachments/assets/3bc124c6-7b84-466a-809d-834e87518d01)

사용자가 인증되면 서버가 토큰을 발급하고 클라이언트는 이후 요청에서 토큰을 사용

토큰은 클라이언트에 저장되며 각 요청시 서버에 전송

서버는 세션 정보를 저장하지 않으며 클라이언트가 전송한 토큰을 검증하여 사용자 식별

### 장점

- 상태 비유지
- 사용자 경험: 토큰은 클라이언트 측에서 저장되기 때문에 매 요청마다 인증 정보를 서버에 보내지 않아도 되어 빠른 인증 속도 제공
- 분리된 인증 서비스: OAuth와 같은 프로토콜을 사용하여 인증 서버와 리소스 서버를 분리 가능

### 단점

- 보안 문제: 토큰이 클라이언트 측에서 탈취 가능 → HTTPS를 사용해야함
- 복잡성: 추가적인 설정과 관리가 필요하며 초기 구현은 세션 기반 인증보다 복잡

### 토큰 기반 인증의 종류

### JWT(JSON Web Token)

- 클레임을 포함하는 JSON 객체로 표현되는 암호화된 토큰
- 헤더, 페이로드, 서명으로 이뤄져 있으며 각 요소는 .으로 구분하여 작성
- 사용자 인증 및 정보 교환에 사용, 토큰에는 사용자 ID, 권한, 만료 시간 등의 정보 포함
- 서버에서 발급된 토큰은 클라이언트에 저장되며
1. 헤더

```jsx
{
  "alg": "HS256", // 토큰이 서명될 때 사용되는 알고리즘
  "typ": "JWT"   // 토큰의 타입 (일반적으로 "JWT" 고정)
}
```

1. 페이로드
- 등록된 클레임
    - 토큰에 대한 정보들을 담기위해 이름이 이미 정해진 클레임
    
    ```jsx
    iss: 토큰 발급자(issuer)
    sub: 토큰 제목(subject)
    aud: 토큰 대상자(audience)
    exp: 토큰의 만료 시간(expiration time)
    nbf: 토큰의 사용 가능 시작 시간(not before)
    iat: 토큰의 발급 시간(issued at)
    jti: JWT의 고유 식별자(JWT ID)
    ```
    
- 공개 클레임
    - JWT 표준에 정의된 것은 아니지만, 일반적으로 사용되는 클레임들
    - 등록된 클레임은 JWT 표준에 명시적으로 정의되어 있지만, 공개 클레임은 표준이 아니며 특정 시스템이나 애플리케이션에서 필요한 정보를 나타내기 위해 사용됨
    
    ```jsx
    auth_time
    acr
    nonce
    ```
    
- 사설 클레임
    - JWT 페이로드에 포함되는 사용자 정의 정보를 나타내는 클레임
    
    ```jsx
    name
    email
    role
    ```
    
1. 서명
- JWT의 서명은 헤더와 페이로드를 결합한 후, 선택된 알고리즘을 사용하여 생성됩니다.
- 서명은 토큰이 변조되지 않았음을 검증하는 데 사용됩니다.
- 예를 들어, HMAC SHA-256 알고리즘을 사용하여 헤더와 페이로드를 서명한 후, 이 서명은 JWT의 세 번째 부분으로 추가됩니다.

```jsx
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwMCIsIm5hbWUiOiJKb2huIERvZSIsImhlbGxvIjoid29ybGQifQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c
```

### OAuth(Open Authorization)

웹, 모바일 앱을 위한 표준 인증 프로토콜

사용자가 리소스 소유자의 인증 정보를 제공하지 않고도 다른 웹 사이트 또는 앱에 대한 접근 권한을 부여할 수 있는 방법 제공

- 인증
    - OAuth는 인증 정보를 제공하지 않고도 사용자가 다른 서비스 또는 앱에 대한 접근 권한을 부여할 수 있는 인증 메커니즘 제공
    - 사용자의 민감한 정보를 노출하지 않고 외부 서비스에 대한 접근 권한 관리 가능
- 인가
    - 사용자가 특정 리소스에 대한 액세스 권한을 부여하거나 거부할 수 있는 기능 제공
    - 앱은 사용자가 선택한 권한 범위 내의 데이터만 접근 가능

### 작동 방식

![image](https://github.com/user-attachments/assets/1b0056f9-0354-47eb-9dbb-7b794d8b9100)

1. 리소스 소유자(Resource Owner): 자원에 접근하려는 사용자, 예를 들어, 소셜 미디어 사이트에서 사용자는 자신의 데이터에 대한 접근 권한을 제어 가능
2. 클라이언트(Client): 사용자의 자원에 접근하려는 애플리케이션 또는 서비스, 예를 들어, 소셜 미디어 앱이나 웹사이트
3. 인증 서버(Authentication Server): 사용자를 인증하고 권한 부여 코드(Authorization Code)를 발급하는 서버, 사용자는 인증 서버를 통해 클라이언트에게 자원 접근 권한을 부여
4. 리소스 서버(Resource Server): 클라이언트가 접근하려는 사용자의 자원을 호스팅하는 서버, 예를 들어, 사용자의 사진이나 프로필 정보를 제공

### 예시

```jsx
// OAuth 2.0 클라이언트 정보
const oauthClient = new oauth2({
    client_id: "your_client_id",
    client_secret: "your_client_secret",
    redirect_uri: "http://localhost:3000/callback/", // 콜백 URL
    authorization_uri: "https://authorization-server.com/oauth/authorize",
    token_uri: "https://authorization-server.com/oauth/token",
});

// 사용자 인증 및 권한 부여
app.get("/authorize", (req, res) => {
    const authorizationUri = oauthClient.authorizeURL({
        redirect_uri: oauthClient.redirect_uri,
        scope: "read write", // 접근 권한(scope) 설정
    });

    res.redirect(authorizationUri);
});
```

```jsx
// 사용자 인증 후 콜백 처리
app.get("/callback", async (req, res) => {
    const { code } = req.query;

    // 토큰 요청
    const tokenParams = {
        code,
        grant_type: "authorization_code",
        redirect_uri: oauthClient.redirect_uri,
    };

    const tokenResponse = await axios.post(oauthClient.token_uri, tokenParams, {
        auth: {
            username: oauthClient.client_id,
            password: oauthClient.client_secret,
        },
    });

    // 토큰을 이용한 API 호출
    const accessToken = tokenResponse.data.access_token;
    const apiResponse = await axios.get("https://api.example.com/data", {
        headers: {
            Authorization: `Bearer ${accessToken}`,
        },
    });

    // API 응답 처리
    res.json(apiResponse.data);
});
```

### SSO(Single Sign-On)

하나의 인증을 통해 여러 시스템 또는 응용 프로그램에 접근할 수 있는 인증 메커니즘

사용자는 단일 인증 과정을 거치며 다양한 서비스에 접근할 수 있으며 각 서비스마다 별도로 로그인할 필요가 없음

### 주요 특징

- 단일 인증: 한 번의 로그인으로 다른 모든 연결된 앱에 접근 가능
- 중앙화된 인증 관리: SSO는 보통 중앙화된 인증 서비스나 ID 관리 시스템을 통해 작동, 사용자의 인증 정보는 한 곳에서 관리되고 다양한 서비스에 전파
- 사용자 경험 향상

### 구현 방식

- OAuth 및 OpenID Connect: 웹 및 모바일 애플리케이션에서 SSO를 구현하는 데 널리 사용되는 프로토콜이며, 클라이언트와 서버 간의 인증 및 인가를 담당
- SAML (Security Assertion Markup Language): 기업 환경에서 널리 사용되는 프로토콜로, XML 기반의 인증 및 권한 부여 데이터를 전달
- LDAP (Lightweight Directory Access Protocol): 기업 내부 인프라에서 사용자 인증 및 디렉터리 서비스를 관리하는 데 사용되며, SSO의 일환으로 구현 가능

### 토큰 기반 인증 시 서버에서 인증 확인 방법

1. 토큰 생성
- 서버에서 사용자 정보를 포함한 토큰 생성
- 보통 사용자 ID, 권한, 만료 시간 등의 정보 포함
1. 토큰을 클라이언트에 전달
- 클라이언트는 토큰을 저장하고 요청 시 서버에 전달
1. 서버에서 토큰 검증
- 토큰 형식 확인 → 서명 검증 → 토큰 만료 시간 확인 → 사용자 권한 정보 확인
1. 인증 확인 및 사용자 정보 로드
- 세션 ID가 유효하지 않다면 인증 실패 반환

# 권한 관리

사용자가 특정 자원이나 기능에 접근할 수 있는 권한을 부여하고 관리하는 프로세스

### 주요 개념

- 권한(Permission): 특정 자원이나 기능에 대한 접근을 허용하는 권한
- 역할(Role): 사용자 그룹에 할당되는 권한의 집합, 비슷한 업무를 수행하는 사용자들을 그룹화하여 권한을 관리
- 정책(Policy): 권한을 관리하기 위해 설정된 규칙이나 지침으로 어떤 사용자가 어떤 자원에 접근할 수 있는지 결정

### 역할 기반 접근 제어(RBAC)

사용자가 수행하는 역할에 기반하여 접근 권한을 관리하는 접근 제어 모델

사용자의 업무 기능에 따라 그룹화된 역할을 할당하고 역할에 따라 특정 자원이나 기능에 접근할 수 있는 권한 부여

- 작동 방식
    - 역할 할당: 관리자는 각 사용자에게 적절한 역할 할당
    - 권한 부여: 각 역할은 특정 자원이나 기능에 대한 권한 할당
    - 역할 관리: 시스템 변화에 따라 역할 관리
- 장점
    - 관리 용이성: 역할 별로 권한을 관리하므로 사용자 별로 직접 권한을 설정할 필요가 없음
    - 보안 강화
    - 비즈니스 요구 사항 충족: 비즈니스 변화에 따라 역할과 권한을 조정하여 요구 사항 충족이 쉬움
- 적용 예시
    - 기업 내부 시스템
    - 금융 서비스
    - 교육 기관
- 코드 예시

```jsx
const express = require("express");
const app = express();
const PORT = 3000;

// 사용자 데이터베이스 (간단하게 하기 위해 하드코딩)
const users = [
    { id: 1, username: "user1", role: "admin" },
    { id: 2, username: "user2", role: "user" },
];

// 미들웨어: 요청이 들어올 때마다 사용자의 역할을 확인하는 함수
function checkRole(role) {
    return function (req, res, next) {
        const user = users.find(u => u.id === req.userId);
        if (!user || user.role !== role) {
            return res.status(403).json({ message: "Forbidden" });
        }
        next();
    };
}

// 예시 API 엔드포인트: 관리자만 접근 가능
app.get("/admin", checkRole("admin"), (req, res) => {
    res.json({ message: "Welcome to admin dashboard!" });
});

// 예시 API 엔드포인트: 모든 사용자 접근 가능
app.get("/public", (req, res) => {
    res.json({ message: "This is a public endpoint." });
});

// 서버 시작
app.listen(PORT, () => {
    console.log(`Server is running on http://localhost:${PORT}`);
});
```

### 속성 기반 접근 제어(ABAC)

사용자의 속성, 대상의 속성, 환경 조건 등 다양한 속성을 기반으로 접근 권한을 결정하는 접근 제어 모델

사용자의 특성과 상황을 더욱 동적으로 반영하여 접근 제어 수행

- 작동 방식
    - 속성 수집: 다양한 속성을 수집하여 평가에 사용
    - 정책 평가: 규칙과 속성을 비교하여 사용자가 요청한 자원에 대한 접근 허용 여부 결정
    - 동적 접근 제어: 사용자 상황에 따라 동적으로 접근 권한 결정 가능
- 장점
    - 동적 접근 제어: 유연성 증대
    - 정확성과 정밀성: 다양한 속성을 고려
    - 복잡한 환경 처리
- 적용 예시
    - 클라우드 환경
    - 금융 서비스
- 코드 예시

```jsx
const express = require("express");
const app = express();
const PORT = 3000;

// 사용자 데이터베이스 (간단히 하기 위해 하드코딩)
const users = [
    { id: 1, username: "user1", department: "IT", location: "office1" },
    { id: 2, username: "user2", department: "HR", location: "office2" },
];

// 미들웨어: 요청이 들어올 때마다 접근 제어를 수행하는 함수
function checkAccess(attribute, value) {
    return function (req, res, next) {
        const user = users.find(u => u.id === req.userId);
        if (!user || user[attribute] !== value) {
            return res.status(403).json({ message: "Forbidden" });
        }
        next();
    };
}

// 예시 API 엔드포인트: IT 부서 직원만 접근 가능
app.get("/it", checkAccess("department", "IT"), (req, res) => {
    res.json({ message: "Welcome to IT department!" });
});

// 예시 API 엔드포인트: office1 위치에 있는 직원만 접근 가능
app.get("/office1", checkAccess("location", "office1"), (req, res) => {
    res.json({ message: "Welcome to office1!" });
});

// 서버 시작
app.listen(PORT, () => {
    console.log(`Server is running on http://localhost:${PORT}`);
});
```

# 인증 보안 관리

## 브루트 포스 공격

가능한 모든 조합을 시도하여 인증을 뚫으려는 공격

### 대응 방안

- 강력한 비밀번호 정책
- 계정 잠금 기능
- IP 차단: 일정 IP범위에서 너무 많은 요청 발생시 해당 IP를 일시적으로 차단

## 세션 하이재킹

![image](https://github.com/user-attachments/assets/caa8afa6-370a-49be-a214-472856c38ca0)

사용자의 세션 ID를 탈취하여 해당 세션으로 접근하려는 공격

### 대응 방안

- HTTPS 사용: 데이터를 암호화하여 중간자 공격 방지, 세션 데이터 안전성 보장
- 세션 유효 시간 관리
- 세션 관리: 보안 쿠키를 사용하거나 사용자 장치 및 IP 주소와 같은 추가 정보를 고려하여 세션을 관리하고 보호

## 암호화

데이터의 기밀성을 보호하기 위해 사용

대표적인 기법으로는 대칭키 암호화, 비대칭키 암호화

### 대칭키 암호화

암호화 복호화에 동일한 키를 사용하는 방식

데이터 전송 시 키를 공유해야하지만 빠르고 효율적

예시: AES

### 비대칭키 암호화

암호화, 복호화에 서로 다른 키를 사용하는 방식

공개키와 개인키를 함께 사용하며 보안성이 뛰어나지만 연산 비용이 높음

예시: RSA

## 해싱

임의의 길이를 가진 데이터를 고정된 길이의 데이터로 매핑하는 알고리즘

해시 함수는 동일한 입력에 대해 항상 동일한 출력 생성

데이터 무결성 검증이나 데이터를 안전하게 저장하는 데 사용

예시: SHA-256

### 비밀번호 해싱

사용자 비밀번호와 같은 중요 정보는 단방향 해시 함수를 사용하여 저장

데이터베이스에 실제 비밀번호를 저장하지 않고 로그인 시 입력된 비밀번호를 해시하여 저장된 해시 값과 비교

해시 함수에 솔팅 기법을 추가하여 보안성 강화 가능

- 중요성
    - 보안 강화: 데이터 유출 시에도 비밀번호 노출 최소화
    - 레인보우 테이블 방지: 솔팅 기법을 사용하여 레인보우 테이블 공격 방지
    - 규정 준수: 개인정보 보호 법규에 따른 보안 요구사항 준수

