## 스프링 빈(Spring Bean)이란?🫛
스프링 빈(Spring Bean)은 스프링 프레임워크에서 관리하는 객체를 의미합니다. 스프링 빈은 애플리케이션의 핵심을 이루는 요소로, 스프링의 제어 역전(IoC, Inversion of Control) 컨테이너에 의해 인스턴스화, 관리, 설정됩니다. 이러한 빈들은 보통 애플리케이션의 비즈니스 로직을 수행하는 컴포넌트, 서비스, 리포지토리 등으로 사용됩니다.


### 스프링 빈의 특징

- **관리**: 스프링 컨테이너에 의해 라이프사이클이 관리됩니다.
- **싱글톤**: 기본적으로 스프링은 각 빈을 싱글톤으로 관리하여, 한 개의 인스턴스만을 생성합니다.
- **연결**: 의존성 주입(DI, Dependency Injection)을 통해 다른 빈들과 연결될 수 있습니다.
- **설정**: XML, 어노테이션, 자바 설정 클래스를 통해 빈을 선언하고 구성할 수 있습니다.

### 스프링 빈의 등록 방법

- **컴포넌트 스캔**: `@Component` 어노테이션과 그 파생형인 `@Service`, `@Repository`, `@Controller`를 사용하여 자동으로 빈을 등록할 수 있습니다.
- **자바 설정 파일**: `@Bean` 애너테이션을 사용하여 명시적으로 빈을 등록할 수 있습니다.

### 스프링 빈의 사용

스프링 빈은 주로 서비스 계층, 데이터 접근 계층, 프레젠테이션 계층 등 애플리케이션의 다양한 계층에서 사용됩니다. 이를 통해 애플리케이션의 모듈화를 증진시키고, 코드의 재사용성과 테스트 용이성을 향상시킬 수 있습니다.


## 스프링 빈 스코프(Bean Scope)에 대하여 🌟

스프링의 빈(Bean) 스코프는 빈이 생존하고, 적용되는 범위를 정의합니다. 각 스코프는 빈의 생명주기와 영향을 받는 범위가 다릅니다. 스프링은 여러 종류의 스코프를 지원하여 다양한 상황에 대응할 수 있도록 합니다.

## 싱글톤 스코프(Singleton Scope) 🏰

싱글톤 스코프는 스프링의 기본 스코프로, 스프링 컨테이너의 생명주기와 동일합니다. (스프링 컨테이너의 시작과 종료까지 유지되는 가장 넓은 범위의 스코프) 이 스코프의 빈을 조회하면, 항상 같은 인스턴스를 반환하여 애플리케이션 전체에 걸쳐 공유됩니다.

```java
@Component
@Scope("singleton")
public class SingletonBean {}
```

## 프로토타입 스코프(Prototype Scope) 🌱

프로토타입 스코프는 요청할 때마다 새로운 인스턴스를 생성합니다. 스프링 컨테이너는 빈의 생성과 의존성 주입까지만 관여하고, 그 이후에는 빈의 생명주기를 관리하지 않습니다.

```java
@Component
@Scope("prototype")
public class PrototypeBean {}
```

## 웹 관련 스코프(Web-Related Scopes) 🌐

웹 애플리케이션에서만 사용되는 스코프들로, HTTP 요청의 생명주기에 따라 빈이 생성되고 소멸합니다.

### 리퀘스트 스코프(Request Scope) 📬

각 HTTP 요청마다 별도의 빈 인스턴스가 생성되고, 요청이 끝나면 소멸합니다. (웹 요청이 들어오고 나갈때 까지 유지되는 스코프)

```java
@Component
@Scope(value = "request", proxyMode = ScopedProxyMode.TARGET_CLASS)
public class RequestScopedBean {}
```

### 세션 스코프(Session Scope) 🛒

HTTP 세션의 생명주기와 동일하게 빈이 유지됩니다. 사용자의 세션마다 별도의 빈 인스턴스가 유지됩니다. (웹 세션이 생성되고 종료될 때 까지 유지되는 스코프)

```java
@Component
@Scope(value = "session", proxyMode = ScopedProxyMode.TARGET_CLASS)
public class SessionScopedBean {}
```

### 애플리케이션 스코프(Application Scope) 🌍

전체 웹 애플리케이션의 서블릿 컨텍스트와 동일한 생명주기를 가지는 스코프입니다.

```java
@Component
@Scope(value = "application", proxyMode = ScopedProxyMode.TARGET_CLASS)
public class ApplicationScopedBean {}
```

### 웹소켓 스코프(WebSocket Scope) 🕸️

웹 소켓 세션의 생명주기에 따라 빈이 유지됩니다.

```java
@Component
@Scope(value = "websocket", proxyMode = ScopedProxyMode.TARGET_CLASS)
public class WebSocketScopedBean {}
```

## 프로토타입 스코프의 주의점 ⚠️

프로토타입 스코프 빈을 싱글톤 빈 안에서 사용할 때, 프로토타입

 빈은 초기 주입 시점에만 새로 생성되며, 이후에는 싱글톤 빈과 생명주기를 공유하게 되어 매번 새로운 객체를 받기 어렵습니다.

## 해결책: ObjectProvider 💡

### 1. 이 문제를 해결하기 위해, `ObjectProvider`를 사용하여 필요할 때마다 새로운 프로토타입 빈을 생성하도록 할 수 있습니다.

 - ObjectFactory : 기능이 단순하다, 별도의 라이브러리가 필요 없으며, 스프링에 의존적입니다.
 - ObjectProvider : ObjectFactory 상속, 옵션, 스트림 처리등 편의 기능이 많고, 별도의 라이브러리가 필요 없으며, 스프링에 의존적입니다.

```java
@Autowired
private ObjectProvider<PrototypeBean> prototypeBeanProvider;

public int logic() {
    PrototypeBean prototypeBean = prototypeBeanProvider.getObject();
    // use prototypeBean
}
```
### 2. `jakarta.inject.Provider`라는 JSR-330 자바 표준을 사용 할 수도 있습니다.

- get() 메서드 하나로 기능이 매우 단순합니다.
- 별도의 라이브러리가 필요합니다.
- 자바 표준이므로 스프링이 아닌 다른 컨테이너에서도 사용 할 수 있습니다.

```java
@Autowired
private Provider<PrototypeBean> prototypeBeanProvider;

public int logic() {
    prototypeBean prototypeBean = prototypeBeanProvider.get();
    // use prototypeBean
}
```
