# 객체지향프로그래밍(Object Oriented Programming)

> 프로그래밍 패러다임 중 일부로 명령형 프로그래밍에 속한다.

## 객체지향 프로그래밍이란?

비슷한 구조를 가진 프로그래밍을 만들때 해당 프로그래밍에 필요한 데이터를 `추상화`시켜 **상태(Property)** **행위(Method)**를 가진 객체를 만들고 만든 객체로부터 상호작용을 통해 로직을 구성하는 프로그래밍 방법이다.

- 상태(Property) : 객체의 상태를 나타내는 값
- 행위(Method) : Property를 참조하면서 어떠한 행위를 하는것

클래스로 예시를 들어보자.

```javascript
class Animal {
  constructor(leg) {
    this.isAlive = true;
    this.leg = leg;
  }

  walk() {
    console.log(`${this.leg}개의 다리로 걷는다.`);
  }
}

const cat = new Animal(4);
console.log(cat.isAlive); //true
console.log(cat.leg); //4
console.log(cat.walk()); //'4개의 다리로 걷는다.'
```

여기서 `cat`은 `Animal`이라는 객체(클래스)로부터 모든 성질을 참조한다. 그리고 `cat`의 다리수를 입력하여 객체와 상호작용을 할 수 있다.

## 객체 지향 프로그래밍의 특징

### 추상화

- 객체에서 공통된 속성과 행위를 추출 하는 것
- 추출한 속성과 행위를 타입을 정의하는 과정
- 불필요한 정보는 숨기고 중요한 정보만 표현함으로써 프로그램을 간단하게 만드는것

```javascript
// 추상화 전
const Audi = {
  brand: 'Audi',
  head: 'Germany',
  wheel: 4
}

const BMW = {
  brand: 'BMW',
  head: 'Germany',
  wheel: 4
}

const Hyundai = {
  brand: 'Hyundai',
  head: 'Korea',
  wheel: 4
}
// 추상화 후
const Car(name, head) {
  this.name = name;
  this.head = head;
  wheel = 4
}
```

javascript 생성자 함수가 예시에 적용되었다.

각각의 객체들의 속성, 행위(위의 예시에는 행위는 없지만)를 추출하고 추상화 시켜 `생성자 함수`를 정의할 수 있다.

이런식으로 추상화를 한다면 나중에 다른 브랜드가 추가될 시 쉽게 정보들을 정의할 수 있다.

### 캡슐화

데이터 구조와 데이터를 다루는 방법들을 결합 시켜 묶는것 (프로퍼티와 메서드를 객체의 형태로 하나로 묶는것을 의미한다.)

낮은 결합도를 유지할 수 있도록 설계하는방법

- 클래스라는 캡슐에 넣어서 분류함으로써 재활용이 원할하다는 장점이 있다.
- 접근제어자(public, private, protected)등을 활용하여 `정보은닉`이 가능하다.

### 상속

클래스의 속성과 행위를 그대로 하위 클래스에 물려줄 수 있다. 이를 `상속`이라고 한다.
상속받은 하위클래스는 상위클래스의 속성과 행위를 사용할 수 있다.

```javascript
class Animal {
  constructor(leg) {
    this.isAlive = true;
    this.leg = leg;
  }

  walk() {
    console.log(`${this.leg}개의 다리로 걷는다.`);
  }
}

class Mammalia extends Animal {
  speak() {
    console.log('wal wal');
  }
}

const dog = new Mammalia();
console.log(dog.isAlive); //true
console.log(dog.speak()); // 'wal wal'
```

👍 장점

- 재사용하는 코드가 줄어든다.
- 범용적인 사용이 가능하다
- 프로퍼티, 메서드를 자유롭게 사용 및 추가가 가능하다

👎 단점

- 상위 클래스의 변경이 어려워진다. (상속을 준 하위클래스에 영향이 가기때문에)
- 불필요한 클래스가 증가한다.

### 다형성

- `오버라이딩` : 상위클래스로부터 상속받은 하위 클래스에서 재정의해서 사용하는 것
- `오버로딩` : 하나의 클래스에서 같은 메서드에서 조건에따라 다른 기능을 하는것

## 객체지향 프로그래밍이의 장단점

👍 장점

- 클래스 단위로 모듈화시켜서 업무 분리가 쉽고 대규모 프로젝트에 적합하다.
- 클래스 단위로 수정이 가능하므로 유지보수가 편리하다
- 클래스의 재사용 또는 상속을 통해 확장이 가능하다

👎 단점

- 설계 단계에 많은 시간과 노력이 필요하다.
- 처리속도가 상대적으로 느리다.
