
# 1. HTTP 헤더

---

## 목적과 중요성
- HTTP 헤더는 웹 통신에서 필수적인 역할. 이들은 클라이언트와 서버 간의 통신을 매개하고, 데이터 전송에 필요한 정보를 제공
- HTTP 헤더를 통해 클라이언트는 요청의 세부 사항을 서버에 전달하고, 서버는 응답의 성격과 콘텐츠를 클라이언트에게 전달할 수 있음. 이러한 헤더는 웹의 성능, 보안, 그리고 사용자 경험에 직접적인 영향을 미침

## 헤더의 유형 소개
HTTP 헤더는 크게 네 가지 주요 유형으로 구분
![](https://velog.velcdn.com/images/k-minsik/post/b8945f00-dcc5-41c9-8917-4a1a4997e98d/image.png)


1. **일반 헤더 (General Header):** 요청과 응답 양쪽 모두에 공통적으로 적용되는 헤더로, 메시지의 전반적인 속성과 통신 세션 관리에 관련된 정보를 담
2. **표현 헤더 (Representation Header):** HTTP 메시지의 본문(페이로드)에 대한 정보를 제공하며, 본문의 타입, 언어, 인코딩 등을 설명
3. **요청 헤더 (Request Header):** 클라이언트가 서버로 보내는 요청에 특화된 정보를 담습니다. 이 헤더는 요청의 종류, 클라이언트의 선호도 등을 서버에 알림
4. **응답 헤더 (Response Header):** 서버가 클라이언트에게 보내는 응답에 특화된 정보를 담습니다. 이 헤더는 응답의 상태, 서버 정보 등을 클라이언트에 제공

---

## 2. 헤더 유형의 상세 설명

### 2.1 일반 헤더 (General Header)
일반 헤더는 요청과 응답 모두에 적용되며, 메시지의 전체적인 속성과 통신 세션을 관리하는 데 사용
![](https://velog.velcdn.com/images/k-minsik/post/c3511e33-1753-420e-a65c-e1432b04bdfb/image.png)


- **Cache-Control**: 캐싱 메커니즘을 지정
  - ex : `no-cache`, `max-age=3600`.
- **Connection**: 현재의 연결에 대한 옵션을 지정
  - ex : `keep-alive`, `close`.
- **Date**: 메시지가 생성된 정확한 날짜와 시간을 나타냄

### 2.2 표현 헤더 (Representation Header)
표현 헤더는 요청과 응답 모두에 적용되며, 메시지의 본문의 내용과 데이터 형식을 표현 (Entity Header)

- **Content-Type**: 메시지 본문의 미디어 타입을 지정
  - ex : `Content-Type:text/html`, `application/json`, `image/png`.
- **Content-Encoding**: 메시지 본문이 어떻게 인코딩되었는지 나타냄, 압축과 압축 해제
   - ex : `Content-Encoding:gzip`, `deflate`.
- **Content-Language**: 메시지 본문의 자연 언어를 지정
  - ex : `Content-Languauge: ko`, `en`, `fr`.
  - **Content-Length**: 메시지 본문의 길이
  - ex : `Content-Length: 5`

### 2.3 요청 헤더 (Request Header)
요청 헤더는 클라이언트가 서버에 보내는 HTTP 요청에 대한 정보를 포함

- **Host**: (필수) 요청이 전송되는 대상 서버의 이름과 포트를 지정
- **User-Agent**: 클라이언트의 애플리케이션, 운영 체제, 브라우저 및 버전 정보를 제공
- **Accept**: 클라이언트가 처리할 수 있는 미디어 타입을 명시
	- `Accept-Charset`, `Accept-Encoding`, `Accept-Language`
- **Authorization**: 클라이언트가 인증 토큰을 서버로 보낼 때 사용
- **Cookie**: 클라이언트가 서버에서 받은 쿠키를 저장, 요청 시 서버로 전달
- **Referer**: 클라이언트의 이전 웹 페이지 주소, 유입 경로 등을 분석 가능


### 2.4 응답 헤더 (Response Header)
응답 헤더는 서버가 클라이언트에게 보내는 HTTP 응답에 대한 정보를 포함

- **Server**: 응답을 보내는 서버의 소프트웨어 및 버전 정보를 제공
  - ex : `Server: nginx`
- **Location**: 페이지 리다이렉션, 상태코드 3XX에서 사용
- **Allow**: 응답을 보내는 서버의 지원 가능한 HTTP 메서드 리스트
	- ex : `Allow : GET, POST`
- **Status-Line**: 응답의 상태를 나타내는 코드와 상태 메시지를 포함
  - ex : `200 OK`, `404 Not Found`.
- **Set-Cookie**: 클라이언트 브라우저에 쿠키를 설정하기 위한 지시어를 포함
