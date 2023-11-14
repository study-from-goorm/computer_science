# 싱글톤 패턴

하나의 클래스는 하나의 인스턴스만 가질 수 있다.

즉, 생성된 하나의 인스턴스만을 사용하여 해당 인스턴스를 다른 모듈들이 공유하면서 사용하는 패턴이다.

ex) DB연결 모듈에서 많이 사용됨

싱글톤 패턴이 아닌경우

```javascript
const obj = {
  a: 27,
};

const obj2 = {
  a: 27,
};

console.log(obj === obj2); // false
```

싱글톤 패턴

```javascript
class Singleton {
  constructor() {
    if (!Singleton.instance) {
      Singleton.instance = this;
    }
    return Singleton.instance;
  }
  getInstance() {
    return this;
  }
}
const a = new Singleton();
const b = new Singleton();
console.log(a === b); // true
```

DB연결 모듈

```javascript
const URL = 'mongodb://localhost:27017/kundolapp';
const createConnection = (url) => ({ url: url });
class DB {
  constructor(url) {
    if (!DB.instance) {
      DB.instance = createConnection(url);
    }
    return DB.instance;
  }
  connect() {
    return this.instance;
  }
}
const a = new DB(URL);
const b = new DB(URL);
console.log(a === b); // true
```

### 싱글톤 패넡의 단점 👎

- TDD를 할때 방해가 된다.
  - 주로 단위로 나누어서 테스트를 하게 되는데 하나의 인스턴스를 바라보고 있기때문에 독립성을 가지기 힘들다.
- 모듈들이 지나치게 결합이 강하다.
  - 메인 모듈이 모든 하위모듈에 대한 의존성을 주기때문이다.
  - 중간단계의 의존성 주입자를 만들어 메인모듈과 하위모듈들의 의존성을 떨어트리는 방법이 있다.`디커플링`

### 의존성 주입의 장점

- 모듈들에게 독립성을 주기때문에 테스팅하거나 마이그레이션이 수월하다.
- 모듈들의 관계가 명확해진다.

### 의존성 주입의 단점

- 그만큼 모듈들이 늘어나고 분리되기 때문에 코드 자체 실행속도 즉, 런타임이 증가한다.
