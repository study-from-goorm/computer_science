## 인증(Authentication)

인증은 사용자가 누구인지 확인하는 과정이다. 

아이디와 비밀번호 입력, 생체 인식, OTP, 스마트 카드와 같은 방법이 있다.

### 특징

- 신원 확인: 사용자의 신원을 확인하는 첫 번째 단계이다.

- 보안 정보: 비밀번호, PIN, 생체 인식 정보 등 사용자만이 알고 있는 정보를 사용한다.

- 다단계 인증: 추가 보안을 위해 두 개 이상의 인증 방법을 사용할 수 있다.

ex) 비밀번호 + OTP

## 인가(Authorization)

인가는 인증된 사용자가 특정 자원이나 서비스에 접근할 수 있는 권한을 부여받는 과정이다. 

예를 들어, 관리자는 시스템의 특정 부분에 대한 접근 권한을 가지지만 일반 사용자는 접근 권한을 가질 수 없다.

### 특징

- 접근 제어: 사용자가 접근할 수 있는 데이터나 자원을 결정한다.

- 역할 기반 접근 제어(RBAC): 사용자의 역할에 따라 접근 권한이 달라진다다.

- 정책 및 규칙: 조직의 보안 정책과 규칙에 따라 접근 권한이 설정된다.


인증 : '누가 사용자인가'

인가 : '사용자가 무엇을 할 수 있는가'
___

## 구현

### 쿠키

![](https://velog.velcdn.com/images/tme2685/post/b3902864-0509-4f4f-be77-6c9ad5f1f3ff/image.png)

#### Response Header
```
HTTP/1.1 302
Date: Tue, 6 Dec 2023 17:10:37 GMT
Set-Cookie: IDPW=test.test!; Max-Age=3600;
...
```
매번 로그인 정보를 요청에 담아 보내는 것은 보안상 문제가 생길 수 있다.

이러한 문제점에서 벗어나고자 나온 것이 Session이다.

### 세션
![](https://velog.velcdn.com/images/tme2685/post/62d4a244-9a68-4342-8a07-e2173189159a/image.png)

중요한 정보를 주고받지 않아 보안상 이점이 있지만, 사용자를 식별할 수 있는 값을 생성하고 서버에 저장해두어야 한다.

#### 만약 서버가 여러 대라면?
![](https://velog.velcdn.com/images/tme2685/post/e478dbae-9949-4a00-816f-b40ce2204542/image.png)

![](https://velog.velcdn.com/images/tme2685/post/7dc56038-1963-461b-b50e-e52159293c77/image.png)

Session ID의 탈취의 가능성이 있고, 무엇보다 Client의 상태를 서버에서 관리한다는 점이 HTTP 통신의 stateless 특성과는 거리가 있다.

### 토큰
사용자를 인증할 수 있는 정보가 숨겨진 암호화된 Access Token을 발행하고, 인증이 필요할 때마다 서버에 Token과 함께 요청을 보낸다.

서버는 저장된 데이터가 아닌 Token 해독을 통해 Token 속에서 사용자를 식별할 수 있는 정보들을 알아내고 이를 바탕으로 인증/인가를 한다.

#### JWT
```
// 예시
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9  // Header 영역
.eyJzdWIiOiIxMjM0NTY3ODkwIiwiaWQiOiJlZ2c1MjgifQ // Payload 영역
.dxx7fHi3twlN_GnfG3kZHxkLElTi9y99n5DEby-a_TE  // Signature 영역
```
Header, Payload, Signature로 구성된 정보들은 "."을 구분자로 위 예시와 같이 읽기 어려운 코드로 생성된다.

```
Jwts.builder()
     .setClaim(claim)	// key, value 쌍으로 정보 저장
     .setIssuedAt(now)	// 발행 시간
     .setExpiration(expiration)	// 유효 시간
     .signWith(key)  // 서명 저장
     .compact();   // 생성
```
