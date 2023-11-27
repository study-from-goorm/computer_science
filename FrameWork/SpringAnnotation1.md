## 스프링 MVC : @ModelAttribute와 @RequestParam 비교하기 🌟

스프링 MVC에서 HTTP 요청을 통해 전송된 클라이언트 데이터를 다루는 일은 일상적인 작업입니다. `@ModelAttribute`와 `@RequestParam`은 요청 데이터를 자바 객체에 바인딩하는 데 자주 사용되는 주요 애노테이션들입니다. 첫눈에 비슷해 보일 수 있지만, 각각 고유한 목적과 행동 방식을 가지고 있습니다.

- 바인딩 : 프로그래밍에서 특정 값을 변수에 할당하거나, 데이터를 어떤 구조에 연결하는 행위 (데이터를 변수나 객체에 '연결하는' 작업)

### @RequestParam이란? 🎯

`@RequestParam`은 URL의 쿼리 파라미터나 POST 요청 본문의 폼 파라미터에서 단일 요청 파라미터를 추출하여 사용합니다. 컨트롤러의 메소드 파라미터에 요청 파라미터를 바인딩합니다.

**핵심 포인트:**
- 단순 데이터 타입(String, int, long 등)을 다루는 데 이상적입니다.
- 하나의 HTTP 요청 파라미터를 메소드의 하나의 파라미터로 매핑합니다.
- 검색 양식, 데이터 필터링, 폼 제출 처리에 주로 사용됩니다.

**예시:**
```java
@GetMapping("/search")
public String search(@RequestParam String query) {
    // 검색 처리 로직
}
```

### @ModelAttribute란? 📦

`@ModelAttribute`는 여러 요청 파라미터를 객체에 바인딩하는 데 더 효율적입니다. 폼에 여러 필드가 있을 경우, `@ModelAttribute`는 도착하는 데이터를 필드 이름이 일치하는 빈(bean)에 매핑합니다.

**핵심 포인트:**
- 폼 파라미터에서 복합 객체를 채우는 데 적합합니다.
- 자동으로 객체를 모델에 추가하여 뷰에서 사용할 수 있게 합니다.
- 폼의 데이터 구조를 나타내는 자바 객체를 다루는 폼 제출에 유용합니다.

**예시:**
```java
@PostMapping("/register")
public String registerUser(@ModelAttribute User user) {
    // 사용자 등록 처리 로직
}
```

### @RequestParam vs @ModelAttribute: 비교하기 🔍

**단순함 vs 복잡함:**
- `@RequestParam`은 간단하고 단일 값을 다룹니다.
- `@ModelAttribute`는 복합 객체를 다루며, 강력하지만 약간 더 복잡합니다.

**바인딩 메커니즘:**
- `@RequestParam`은 개별 쿼리나 폼 파라미터를 바인딩합니다.
   - GET - 쿼리 파라미터[개별 쿼리], POST - HTML Form[폼 파라미터]
- `@ModelAttribute`는 관련된 모든 요청 파라미터를 객체의 필드에 바인딩합니다.
   - 위 예시로 보았을 때, user 객체의 필드에 바인딩

**애노테이션 대상:**
- `@RequestParam`은 메소드 파라미터에 적용됩니다.
- `@ModelAttribute`는 메소드 파라미터 뿐만 아니라 메소드 자체에도 사용될 수 있습니다.
   - 강의에서 메소드 자체 사용은 다루지 않았습니다.

**사용 상황:**
- 단순한 폼 요소나 쿼리 파라미터를 검색할 때 `@RequestParam`을 권장합니다.
- 폼 제출을 처리하고 객체 모델에 직접 매핑되는 경우 `@ModelAttribute`을 권장합니다.

### 정리 🌈

`@ModelAttribute`와 `@RequestParam` 사이의 미묘한 차이점을 이해하는 것은 효과적인 스프링 MVC 개발에 중요합니다.

`@RequestParam`은 단순한 시나리오에 완벽하며, `@ModelAttribute`는 객체 바인딩 및 데이터 조작을 필요로 하는 시나리오에서 빛납니다. 상황에 맞게 현명하게 선택하여, 스프링 MVC에서 요청 데이터를 능숙하게 관리할 수 있을 것입니다.

---

### `LV.1` HttpServletRequest를 사용할 때 (with HttpServletResponse)
```java
@RequestMapping("/servlet-request")
public void servletRequest(HttpServletRequest request,HttpServletResponse response) throws IOException {
    
    String username = request.getParameter("username");
    int age = Integer.parseInt(request.getParameter("age"));
    

    response.getWriter().write("ok");
}
```
- 자바만 사용할 시에는 꽤 복잡한 모습을 보여줍니다.
   - 파라미터를 받아올 때도 `getParameter()`을 사용해야하고
   - 응답을 보낼때도 `getWriter()`을 사용해야 합니다.



### `LV.2` @RequestParam을 사용할 때 (with @ResponseBody)
```java
@ResponseBody
@RequestMapping("/request-param")
public String requestParam(
        @RequestParam("username") String memberName,
        @RequestParam("age") int memberAge) {

    return "ok";
}
```
- 단, HTTP 파라미터 이름이 변수 이름과 같으면 변수명 생략 가능합니다.
   - [ex] "username"이 "memberName"과 같다면 "username"생략가능
- String, int, Integer 등의 단순 타입이면 @RequestParam도 생략 가능합니다.
   - 너무 없는 경우는 과하다는 생각 때문에 권장하지 않음.
- defaultValue를 추가하여 기본값을 적용 할 수 있습니다.
   - `@RequestParam(defaultValue = "1") int count`
   -  null값이거나 빈문자일때 기본값 1을 적용함.
- 파라미터를 Map형식으로도 조회 할 수 있습니다.
   - `@RequestParam Map<String, Object> paramMap`
   - 파라미터의 값이 1개가 확실하면 Map 아니면 MultiValueMap
- `@ResponseBody`를 사용함으로 HTTP message body에 직접 내용 입력 가능합니다.
   - View조회 무시 String형태로 간단하게


### `LV.3` @ModelAttribute를 사용할 때 (with @ResponseBody)
```java
@ResponseBody
@RequestMapping("/model-attribute")
public String modelAttribute(@ModelAttribute UserData userData) {

    return "ok";
}
```
- 만약 `@RequestParam`이 단순 타입이 아니었다면...?
   - UserData 객체를 생성하고 프로퍼티를 생성해야함
   - 하지만 `@ModelAttribute`를 사용함으로 모두 해결되었습니다.
- `@ModelAttribute` 역시 생략 가능합니다.
   - `@RequestParam` 또한 생략 가능하기에 혼란 발생 가능
