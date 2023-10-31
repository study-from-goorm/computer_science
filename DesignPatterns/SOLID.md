# SOLID란?

Robert C. Martin이 만든 유지보수와 확장이 쉬운 소프트웨어 디자인을 위한 원칙들의 첫 글자를 딴 단어이다.

## 1. 단일 책임 원칙 (SRP)

클래스는 변경되어야 하는 하나의 이유만 가져야 한다.

**예시:**

```java
// SRP 위반
class Report {
    String generateReport(Data data) {
        // 보고서 생성 로직
    }

    void printReport(String report) {
        // 보고서 출력 로직
    }
}

// SRP 준수
class ReportGenerator {
    String generateReport(Data data) {
        // 보고서 생성 로직
    }
}

class ReportPrinter {
    void printReport(String report) {
        // 보고서 출력 로직
    }
}
```

첫 번째 예시에서 `Report` 클래스는 보고서 생성과 출력을 모두 처리하여 SRP를 위반한다.

두 번째 예시에서는 이러한 책임이 두 개의 클래스로 나누어져 SRP를 준수한다.

## 2. 개방/폐쇄 원칙 (OCP)

새로운 기능을 위해 확장할 수 있어야 하지만 변경은 없어야 한다.

**예시:**

```java
// 개방/폐쇄 원칙
interface Shape {
    double calculateArea();
}

class Rectangle implements Shape {
    double length;
    double width;

    @Override
    public double calculateArea() {
        return length * width;
    }
}

class Circle implements Shape {
    double radius;

    @Override
    public double calculateArea() {
        return Math.PI * radius * radius;
    }
}
```

새로운 도형을 추가하더라도 기존 코드를 변경하지 않아도 되므로 OCP를 준수한다.

## 3. 리스코프 치환 원칙 (LSP)

하위 클래스 객체가 상위 클래스 객체를 대체해도 프로그램에 영향이 없어야 한다.

**예시:**

```java
// 리스코프 치환 원칙
class Bird {
    void fly() {
        // 날기 구현
    }
}

class Sparrow extends Bird { }

class Ostrich extends Bird {
    @Override
    void fly() {
        throw new UnsupportedOperationException("타조는 날 수 없습니다");
    }
}
```

`Ostrich` 클래스는 `Bird` 클래스가 만든 행동을 변경하여 LSP를 위반한다.

LSP를 준수하려면 `FlyingBird`와 `NonFlyingBird` 클래스로 나누어야 한다.

## 4. 인터페이스 분리 원칙 (ISP)

포괄적인 인터페이스 대신 클라이언트의 목적과 용도에 적합한 인터페이스 만을 사용해야 한다.

**예시:**

```java
// 인터페이스 분리 원칙
interface Worker {
    void work();
   

 void eat();
}

class HumanWorker implements Worker {
    @Override
    void work() {
        // 일하는 구현
    }

    @Override
    void eat() {
        // 먹는 구현
    }
}

class RobotWorker implements Worker {
    @Override
    void work() {
        // 일하는 구현
    }

    @Override
    void eat() {
        throw new UnsupportedOperationException("로봇은 먹지 않습니다");
    }
}
```

여기서 `RobotWorker`는 필요하지 않은 메소드를 구현해야 하므로 ISP를 위반하고 있다. 

인간과 로봇, 각각의 인터페이스를 만들면 ISP를 준수할 수 있다.

## 5. 의존성 역전 원칙 (DIP)

높은 수준 모듈이 낮은 수준 모듈에 의존해서는 안되며, 추상화에 의존해야 한다.

**예시:**

```java
// 의존성 역전 원칙
interface Switchable {
    void turnOn();
    void turnOff();
}

class LightBulb implements Switchable {
    @Override
    void turnOn() {
        // 전구 켜기
    }

    @Override
    void turnOff() {
        // 전구 끄기
    }
}

class Switch {
    private Switchable device;

    Switch(Switchable device) {
        this.device = device;
    }

    void operate() {
        // 장치 켜기/끄기
    }
}
```

여기서 `Switch` 클래스는 특정 전구 클래스가 아닌 `Switchable` 인터페이스에 의존하므로 DIP를 준수하고 있다.

>객체 지향 설계 원칙인 SOLID가 얘기하는 핵심은 결국 추상화와 다형성
