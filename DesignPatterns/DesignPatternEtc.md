# 나머지 디자인 패턴

## 프록시 패턴

---

대상 객체(Subject)에 접근하기 전 `프록시 객체`가 인터페이스 역할을 하는 디자인 패턴

ex) 보안, 데이터 검증, 캐싱, 로깅등에 사용된다.

### 프록시 서버

> 클라이언트 - 프록시 서버 - 서버

#### Nginx

> 사용자 - Nginx - Web Server - Database

- 익명의 사용자로부터 직접적인 서버의 접근을 막을 수 있다.

### Cloudflare

ex) CDN

- DDOS 공격으로부터 방어
- HTTPS 구축
  - 별도의 인증서 설치 없이 좀 더 쉽게 구축이 가능하다.

#### CORS

여기서 Origin이란, `프로토콜  + 호스트 + 포트번호`를 의미한다.

ex) https://google.com

서버가 웹 브라우저에서 다른 리소스를 로드할때 다른 **오리진**을 통해 로드하지 못하게 하는 메커니즘
즉, CORS설정으로 해당 에러를 해결해 나갈 수 있다.

CORS설정하는 방식이 프록시 패턴 방식을 사용한다.

클라이언트에서 또는 리소스를 가져오는 서버(주로 여기서) CORS설정을 해준다.

ex) GET, HEAD, POST - simple request

ex) PUT, DELETE, PATCH 등 - `preflight` -> cors설정이 되어있는지 미리 체크함

## 이터레이터 패턴

---

```javascript
const mp = new Map();
mp.set('a', 1);
mp.set('b', 2);
mp.set('c', 3);
const st = new Set();
st.add(1);
st.add(2);
st.add(3);

for (let a of mp) console.log(a);
// ['a', 1] ['b', 2] ['c', 3]
for (let b of st) console.log(b);
// 1 2 3
```

해당요소가 이터러블이기 떄문에 순회가 가능하다.
이터러블 - 이터레이터 프로토콜을 따르기 때문에 다음과 같이 순회가 가능한데 이를 이터레이터 패턴이라고 한다.

## 노출 모듈 패턴

접근제어자 public, private, protected을 만드는 패턴

### 즉시 실행함수

```javascript
const foo = (() => {
  const a = 1;
  const b = () => 2;
  const bar = () => {
    c: 2;
    d: () => 3;
  };
  return bar;
})();

console.log(foo.a);
```

private 요소에 접근하지 못함

```javascript
class Person {
  #name = '';

  constructor(name) {
    this.#name = name;
  }

  get gettername() {
    return this.#name.trim();
  }
}

const me = new Person('Lee');
console.log(me.name); // undefined
console.log(me.gettername); //'Lee'
```

## MVC 패턴

## MVP 패턴

Controller 대신 `Presenter`가 사용되는 패턴
뷰와 일대일 대응이 되는 구조로 좀 더 강한 결합을 지닌 디자인 패턴이다.

## MVVM 패턴

Controller 대신 `View Model`가 사용되는 패턴

View Model과 View는 양방향으로 **데이터 바인딩** 및 **커맨드**를 지원한다.
함수를 사용하지않고 ViewModel에서 값 대입만으로 변수가 변경된다.

ex)Vue.js
