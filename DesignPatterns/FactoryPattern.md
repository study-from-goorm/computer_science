# 팩토리 패턴

객체를 사용하는 코드에서 객체 생성부분을 떼어내서 `추상화`한 패턴이다.

상속관계에 있는 상위 - 하위클래스에서 상위클래스가 중요한 뼈대를 결정하고 하위클래스에서 객체 생성에 관한 구체적인 내용을 결정하는 패턴이다.

역할의 분리는 유지보수성을 증가시켜준다.

```javascript
const num = new Object(42);
const str = new Object('avc');

num.constructor.name; // Number
str.constructor.name; // String
```

동일하게 객체를 만들어주는 클래스이지만 입력한 값에 따라 데이터 타입을 지정해주고 있다.

```javascript
class CoffeeFactory {
  static createCoffee(type) {
    const factory = factoryList[type];
    return factory.createCoffee();
  }
}
class Latte {
  constructor() {
    this.name = 'latte';
  }
}
class Espresso {
  constructor() {
    this.name = 'Espresso';
  }
}

class LatteFactory extends CoffeeFactory {
  static createCoffee() {
    return new Latte();
  }
}
class EspressoFactory extends CoffeeFactory {
  static createCoffee() {
    return new Espresso();
  }
}
const factoryList = { LatteFactory, EspressoFactory };

const main = () => {
  // 라떼 커피를 주문한다.
  const coffee = CoffeeFactory.createCoffee('LatteFactory');
  // 커피 이름을 부른다.
  console.log(coffee.name); // latte
};
main();
```

`CoffeeFactory` 상위클래스가 뼈대를 결정하고 하위클래스 `LatteFactory`, `EspressoFactory`가 구체적인 내용을 결정하고 있다.
