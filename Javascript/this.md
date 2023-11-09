# This

객체지향 프로그래밍에서의 객체는 객체의 상태값을 나타내는 `property`와 property를 참조하면서 특정한 동작을한느 `method`로 구성된 자료구조이다.

그럼 method에서 해당 객체에 있는 property 참조하려면 우선 속해있는 객체를 우선 참조할 수 있어야 한다. 그럴때 사용하는것이 바로 **This** 이다.

```javascript
const person = {
  name: 'John',
  sayhi: function () {
    console.log(`hi, may name is ${this.name}`);
  },
};

console.log(person.sayhi());
```

위의 예제에서 사용된 this는 무엇을 가르키는 걸까?

바로 `person`이라는 객체를 가르키고 있다는것을 짐작할 수 있다.

이는 **this가 person 객체에 바인딩**되었다라고 표현 할 수 있다.

기본적으로 this가 바인딩 되는 객체는 다음과 같다.

### 1. 자신이 속한 객체

```javascript
function foo() {
  console.log(this);
}

foo(); // window 객체

const person = {
  name: 'John',
  sayHi: function () {
    console.log(this);
  },
};

person.sayHi(); //{ name: 'John', sayHi: ƒ sayHi() }
```

첫번째 예시는 일반함수로 전역으로 선언되어 있는경우다. 전역으로 선언된 함수는 전역객체(window 객체)에 속해 있다. 그래서 this는 전역객체에 바인딩 된다.

두번째 예시는 person 의 property sayHi에 속해 있는 함수이다. 해당함수는 person이라는 객체에 속해 있기 때문에 this는 person객체에 바인딩 된다.

### 2. 생성예정인 인스턴스 (생성자 함수, 클래스)

```javascript
function Person(age){
  this.name: 'John',
  this.age: age
}

const person = new Person(20);

// {name: 'John', age: 20}
```

생성자함수에서 사용된 this는 생성된 인스턴스를 의미한다.

### 3. 해당 이벤트 currentTarget (Event)

```javascript
btnEl.addEventListener('click', function (e) {
  console.log(thsi === e.currentTarget); // true
});
```

이벤트에서 this는 선택된 이벤트 객체의 currentTarget을 의미한다.

`this`가 3가지 케이스로 바인딩되는 규칙이 명확히 나눠지는것 같지만 사실은 원리는 하나이다.

바로 메서드가 생성될때가 아닌 `호출(실행)`될때 this가 바인딩 되는 객체는 `동적`으로 정해진다는 것이다.

### 1. 일반함수

```javascript
function foo() {
  console.log(this);
}

foo(); // window 객체
```

위의 예제를 다시 살펴보자.

`foo`함수를 호출할때 전역에서 호출을 진행하고 있다. 그러니 전역객체(window)가 this에 바인딩 되는것이다.

### 2. 메서드 호출

```javascript
const obj = {
  foo: function () {
    console.log(this);
  },
};

obj.foo(); //{ foo: ƒ foo() }
```

똑같은 foo함수이지만 foo라는 프로퍼티로 obj에 할당하였고 호출시점에서 obj를 통해서 호출하고 있다.
따라서 **this**는 `obj객체` 바인딩 된다.

### 3. 생성자 함수

```javascript
function Person(age) {
  (this.name = 'John'), (this.age = age);
}

const person = new Person(20);

console.log(person); //
console.log(person.age); //
```

생성자 함수일때의 경우도 다시 살펴보자.

생성자 함수Perosn이 인스턴스를 생성하기전까진 this는 아무것도 바인딩하지 않는다.
하지만 `person`이라는 변수에 인스턴스 생성결과를 할당할때 즉, 정확히 인스턴스를 생성시에 this는 생성되는 새로운 인스턴스 객체를 바인딩하게 된다.

## This Binding의 문제

현실에 있을법한 문제를 예시로 살펴보자

```javascript
const person = {
  age: 20,
  speak(callback) {
    setTimeout(callback, 100);
  },
};

person.speak(function () {
  console.log(`my age is ${this.name}`);
});
```

speak프로퍼티는 callback함수를 매개변수로 받는다. speak함수가 호출되는 시점에 새롭게 콜백함수를 선언한다. 여기서의 콜백함수는 일반함수이고 전역객체에 속해있다. 따라서 this는 window 객체에 바인딩이 되므로 원하는 결과를 도출할 수 없다.

### 해결책

```javascript
const person = {
  age: 20,
  speak(callback) {
    const that = this;
    setTimeout(callback(that), 100);
  },
};

person.speak(function (that) {
  console.log(`my age is ${that.age}`);
});
```

새로운 변수에 원하는 객체가 바인딩 된 this를 할당하여 매개변수로 사용하는 방법이다.

```javascript
const person = {
  age: 20,
  speak(callback) {
    setTimeout(callback, 100);
  },
};

person.speak(
  function () {
    console.log(`my age is ${this.age}`);
  }.bind(person),
);
```

Function.prototype.apply or call or bind 메서드를 활용하는 방법이 있다.

```javascript
const person = {
  age: 20,
  speak() {
    setTimeout(() => {
      console.log(`my age is ${this.age}`);
    }, 100);
  },
};

person.speak();
```

화살표 함수(es6)를 활용하는 방법이 있다. 화살표 함수는 this를 새롭게 객체에 바인딩하지않고 상위스코프에서 바인딩 객체를 그대로 사용한다.
