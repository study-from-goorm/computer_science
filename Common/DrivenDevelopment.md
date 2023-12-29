# Test, Behavior And Domain Driven Development

---

## 테스트 주도 개발 (TDD, Test Driven Development)
![Alt text](image.png)
- **정의** : TDD는 개발 과정에서 테스트를 먼저 작성하고, 이 테스트를 통과할 수 있는 코드를 작성하는 방식
- **목적** : 코드의 신뢰성과 유지 보수성을 높이는 것
- **프로세스** : 
    1. 실패하는 단위 테스트를 먼저 작성
    ```java
    @Test
    public void testAddition() {
        Calculator calculator = new Calculator();
        int result = calculator.add(5, 3);
        assertEquals(8, result);
    }
    ```
    2. 테스트를 통과하기 위한 최소한의 코드를 작성
    ```java
    public class Calculator {
        public int add(int a, int b) {
            return a + b;
        }
    }
    ```
    3. 코드를 리팩토링하여 개선

- **장점** :
    1. 요구사항 이해도 향상
    2. 기존 기능 정상 동작 확인 가능
    3. 코드 리팩토링
- **단점** :
    1. 코드량 증가
    2. 진입장벽
    3. 주객전도

---

## 도메인 주도 개발 (DDD, Domain Driven Desing)
**도메인(Domain)** : 사전적 의미로 영역, 집합, 유사한 업무의 집합
- **정의** : 데이터 중심의 접근법을 탈피하여 순수한 도메인의 모델과 로직에 집중하여 개발에 접근 (도메인을 서비스 별로 분리, MicroService)
- **목적** : 도메인의 복잡성을 관리하고, 소프트웨어가 비즈니스 요구 사항을 충족시키도록 하는 것
- **특징** :
  - 도메인 모델을 중심으로 소프트웨어를 설계
  - 보편적인 언어의 사용을 추구하여, 도메인 전문가와 개발자 간의 긴밀한 협력을 강조
```java
public class Order {

    private OrderId id;
    private Customer customer;
    private List<OrderLine> orderLines;
    private OrderStatus status;

    public Order(Customer customer) {
        this.customer = customer;
        this.orderLines = new ArrayList<>();
        this.status = OrderStatus.NEW;
    }

    public void addOrderLine(Product product, int quantity) {
        OrderLine line = new OrderLine(product, quantity);
        orderLines.add(line);
    }

    ...
}
```


---

## 행동 주도 개발 (BDD, Behvior Driven Development)
- **정의** : BDD는 소프트웨어의 기능이 사용자의 행동에 초점을 맞추도록 하는 시나리오 기반 개발 방법론
- **목적** : 사용자 중심의 소프트웨어 개발을 촉진하고, 명확한 커뮤니케이션을 통해 개발과 요구 사항 간의 간극을 줄이는 것
- **특징** :
  - 사용자의 행동과 요구 사항을 명확하게 이해하는데 중점
  - `Given - When - Then` 과 같은 언어를 사용하여 행동을 설명
```java
@Given("I have a calculator")
public void i_have_a_calculator() {
    calculator = new Calculator();
}

@When("I add {int} and {int}")
public void i_add_and(int a, int b) {
    result = calculator.add(a, b);
}

@Then("the result should be {int}")
public void the_result_should_be(int expected) {
    assertEquals(expected, result);
}
```