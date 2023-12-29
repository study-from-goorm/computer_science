# DI와 DIP
- 의존성 주입(DI, Dependency Injection)이란 메인 모듈(main module)이 '직접' 다른 하위 모듈에 대한 의존성을 주기보다는 중간에 의존성 주입자(dependency injector)가 이 부분을 가로채 메인 모듈이 '간접'적으로 의존성을 주입하는 방식
![](https://velog.velcdn.com/images/k-minsik/post/82827dcb-9016-4635-8ade-52657bf7f7dc/image.png)


- 이를 통해 메인 모듈과 하위 모듈간의 의존성을 조금 더 느슨하게 만들 수 있으며 모듈을 **쉽게 교체 가능한 구조**로 만듬

## 의존한다
- A가 B에 의존한다 = B가 변하면 A에 영향을 미치는 관계 = A -> B 를 의미
- 코드로는 이러한 것을 A가 B에 의존한다고 함

```java
class B {
    public void go() {
        System.out.println("B의 go() 함수");
    }
}

class A {
    public void go() {
        new B().go();
    }
}

public class main {
    public static void main(String args[]) {
        new A().go();
    }
}
// B의 g() 함수
```
---

## 자바 - Project에 DI를 적용하지 않은 사례
![](https://velog.velcdn.com/images/k-minsik/post/065a4402-8ddf-4c57-aff2-4bbd5ebcc3bc/image.png)


```java
class BackendDeveloper {
    public void writeJava() {
        System.out.prinln("Java Server Developer");
    }
}

class FrontendDeveloper {
    public void writeJavascript() {
        System.out.println("React Developer");
    }
}

public class Project {
    private final BackendDeveloper backendDeveloper;
    private final FrontEndDeveloper frontEndDeveloper;
    
    public Project(BackendDeveloper backendDeveloper, FrontEndDeveloper frontEndDeveloper) {
        this.backendDeveloper = backendDeveloper;
        this.frontEndDeveloper = frontEndDeveloper;
    }
    
    public void implement() {
        backendDeveloper.writeJava();
        frontEndDeveloper.writeJavascript();
    }

    public static void main(String args[]) {
        Project a = new Project(new BackendDeveloper(), new FrontEndDeveloper());
        a.implement();
    }
}
```

## 자바 - 자바 - Project 의 DI 적용한 사례
![](https://velog.velcdn.com/images/k-minsik/post/ef16e6a1-d1b5-44c9-b109-1efe98aa608d/image.png)

- DI를 적용한 모습
- 여러명의 개발자를 추가할 수도 있으며 다른 IOS 개발자 등으로 교체도 쉽게 할 수 있는 구조임을 보여줌
- 의존적인 화살표가 '역전'된 것을 볼 수 있음
- DI를 하게 되면 의존관계역전원칙(Dependency Inversion Principle)이 적용되는 것

```java
interface Developer {
    void develop();
}

class BackendDeveloper implements Developer {
    @Override
    public void develop() {
        writeJava();
    }

    public void writeJava() {
        System.out.println("Java Server Developer");
    }
}

class FrontendDeveloper implements Developer {
    @Override
    public void develop() {
        writeJavascript();
    }

    public void writeJavascript() {
        System.out.println("React Developer");
    }
}

public class Project {
    private final List<Developer> developers;
    
    public Project(List<Developer> developers) {
        this.developers = developers;
    }

    public void implement() {
        developers.forEach(Developer::develop);
    }

    public static void main(String args[]) {
        List<Developer> dev = new ArrayList<>();
        dev.add(new BackendDeveloper());
        dev.add(new FrontendDeveloper());
    
        Project a = new Project(dev);
        a.implement();
    }
}
```
---

## 의존관계 역전 원칙
- 의존성 주입을 할 때는 의존관계 역전 원칙(DIP, Dpendency Inversion Principle)이 적용 됨
- **상위 모듈과 하위 모듈의 관계** : 상위 모듈(고수준 모듈)은 하위 모듈(저수준 모듈)에 의존해서는 안 됨. 대신, 두 모듈 모두 추상화에 의존해야 함. 이는 상위 모듈이 하위 모듈의 구현 세부 사항에 직접적으로 의존하지 않게 함으로써 모듈 간의 결합도를 낮춤
- **추상화와 세부 사항의 관계** : 추상화는 세부 사항에 의존해서는 안 되며, 세부 사항은 추상화에 의존해야 함. 즉, 인터페이스(추상화)는 구현 세부 사항(하위 모듈)에 의존하지 않아야 하며, 구현은 인터페이스에 맞춰져야 함
## 의존성 주입의 장점
- **모듈 교체 용이성** : 외부에서 모듈을 생성하고 주입하는 구조는 모듈 교체를 쉽게 할 수 있게 해줌. 이를 통해 코드의 재사용성과 유지보수성이 향상됨
- **단위 테스팅 용이성** : 의존성 주입을 사용하면 테스트를 위한 목(mock) 객체나 스텁(stub) 객체를 쉽게 주입할 수 있어 단위 테스팅이 용이해짐
- **마이그레이션 용이성** : 다양한 환경(예: 다른 데이터베이스)으로의 마이그레이션 시 필요한 변경 사항을 적용하기 쉬워짐
- **코드의 일관성** : 의존성 방향이 일관되어 코드를 이해하고 추론하기 쉬워짐
  
## 의존성 주입의 단점
- **복잡도 증가** : 의존성 주입을 위한 추가적인 코드와 모듈이 필요하게 되어 전반적인 시스템의 복잡도가 증가할 수 있음
- **런타임 에러의 가능성** : 의존성 주입은 주로 런타임에 이루어지므로, 컴파일 타임에는 이러한 의존성 문제를 발견하기 어려울 수 있음

</br>
</br>

> 참고 및 출처 : 인프런 - CS 지식의 정석 | 디자인패턴, 큰돌
https://www.inflearn.com/course/lecture?courseSlug=%EA%B0%9C%EB%B0%9C%EC%9E%90-%EB%A9%B4%EC%A0%91-cs-%ED%8A%B9%EA%B0%95&unitId=118490&tab=curriculum