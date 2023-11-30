## Http는 무엇인가?

`Hyper Text Transfer Protocol`

### 웹상에서 클라이언트와 서버사이에 데이터를 주고받기위한 통신 프로토콜이다.

- Request, Response 구조를따른다.

  - Request: method, path, header, body
  - Response: status code, status message, header, body

- TCP / IP 기반으로 작동한다

- Https
  - Http로 주고받는 자원은 text형식이기 때문에 정보노출을 시키지않기 위해선 `Https`가 필요하다.
 
- Connectless -> Stateless
  - 많은 수의 동시접속을 막아준다.
  - 대신에 브라우저에서 jwt, session, cookie 와 같이 추가작업이 필요하다.

### Method 종류

#### GET

클라이언트가 서버에게 리소스를 요청할때 사용하는 메서드이다.

특정 리소스를 요청하는 방법은 크게 2가지가 있다.

1. `Path Parameter`

```json
// GET http://localhost:3000/fruits
{
  "results": [
    {
      "id": 1,
      "name": "apple",
      "price": 1000
    },
    {
      "id": 2,
      "name": "banana",
      "price": 5000
    },
    {
      "id": 3,
      "name": "grape",
      "price": 5000
    },
    {
      "id": 4,
      "name": "kiwi",
      "price": 7000
    }
  ]
}
// GET http://localhost:3000/fruits/1
 {
  "id": 1,
  "name": "apple",
  "price": 1000
}
```

특정 데이터 전체를 요청하는 경우에 사용된다.

2. `Query String`

```json
// GET http://localhost:3000?price=5000
{
  "id": 2,
  "name": "banana",
  "price": 5000
},
{
  "id": 3,
  "name": "grape",
  "price": 5000
}

// GET http://localhost:3000?price=5000&id=2
{
  "id": 2,
  "name": "banana",
  "price": 5000
}
```

좀더복잡한 조건이 가능하다. `filtering`, `sorting`, `searching`에 적합하다.

#### POST

서버에게 데이터 처리를 요청할때 데이터 생성이 주를 이른다.
body에 데이터를 json형식으로 담아서 전달하는것이 일반적이다.

````javascript
const data = {
    name: "John Doe",
    age: 30,
    email: "johndoe@example.com"
};

fetch('https://your-api-url.com/endpoint', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json',
    },
    body: JSON.stringify(data)
})
.then(response => response.json())
.then(data => {
    console.log('Success:', data);
})
.catch((error) => {
    console.error('Error:', error);
});```
````

#### PUT vs PATCH

- PUT method는 리소스의 `모든것`을 업데이트한다.

```javascript
{
  name: 'kim',
  age: 18,
  location: 'seoul'
}

// PUT method를 통해 age 정보만 업데이트 한경우

{
  age: 20,
}
```

- PATCH method는 리소스의 `일부분만`을 업데이트한다.

```javascript
{
  name: 'kim',
  age: 18,
  location: 'seoul'
}

// PATCH method를 통해 age 정보만 업데이트 한경우

{
  name: 'kim',
  age: 20,
  location: 'seoul'
}
```

### Status Code에 관하여

- 1xx: 정보전달
- 2xx: 성공
- 3xx: 리다이렉션 -> 요청성공을 위해선 추가적인 조치가 필요함
- 4xx: Client Error
- 5xx: Server Error

- 200 : 클라이언트의 요청이 성공적으로 수행됨
- 201 : 리소스의 생성이 성공적으로 수행됨
- 400 : `Bad Request` 전송하는 데이터 형식이 잘못되었음
- 401 : `Unauthorized` 인증이 필요한 상태 (ex. 로그인이 되지 않은 상태)
- 403 : `Forbidden` 권한이 없는 상태
- 500 : `Bad Gateway`

### Network 관점에서 웹사이트 방문설명하기

유저가 브라우저에서 url을 입력하면 어떤 과정을 거쳐 해당 페이지가 나타나는가?

1. 사용자가 url을 입력하면 DNS를 통해 해당 `server ip`를 알아낸다.
2. 해당 주소에게 http request message 전송 요청 -> 요청메시지에 헤더를 추가해서 TCP/IP 패킷 생성
3. 해당 패킷은 랜선을 통해 네트워크로 전송 목적지 `server ip`도착
4. 해당 패킷을 unpacking하고 http 요청메시지에 대한 response data를 바탕으로 http 응답메시지 생성
5. 전달받은 방식 그대로 `client ip`로 전송
6. 전달받은 데이터를 토대로 브라우저에서 `렌더링 작업`
