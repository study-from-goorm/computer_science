# 1. Chrome의 다중 프로세스 아키텍쳐

## 🪐 프로세스와 스레드

- 프로세스 : ‘실행중’인 프로그램
  보조기억장치에 저장되어 있던 프로그램을 메모리에 적재 & 실행하는 순간 프로그램은 ‘프로세스’가 된다.
- 스레드 : 프로세스를 구성하는 실행 흐름 단위 (프로세스 내부에서 프로그램의 일부를 실행)

![https://wd.imgix.net/image/T4FyVKpzu4WKF1kBNvXepbi08t52/x5h2ZL6SWI1vF5jSa8YB.svg](https://wd.imgix.net/image/T4FyVKpzu4WKF1kBNvXepbi08t52/x5h2ZL6SWI1vF5jSa8YB.svg)

💽 애플리케이션 시작

    → 프로세스 하나가 생성됨 (경우에 따라 스레드 생성)
    → 운영체제는 프로세스가 작업할 메모리를 할당
    → 애플리케이션을 종료하면, 프로세스는 사라지고 운영체제는 메모리를 비운다.

하나의 애플리케이션이 여러 개의 프로세스를 갖는 경우 : 경우에 따라 두 프로세스 간 정보 공유가 필요

    ❓ IPC(Inter Process Communication; 프로세스 간 통신)
        - 프로세스들 사이에 서로 데이터를 주고 받는 방식
        - 독립된 메모리 영역을 갖는 서로 다른 프로세스들은 운영체제 커널영역에서 제공하는 IPC 모델 방식을 사용해 통신한다.

→ 특정 작업 프로세스가 응답하지 않을 때, 애플리케이션의 다른 부분을 실행하는 프로세스를 중지하지 않고도 **응답하지 않는 프로세스만 ‘부분적으로’ 다시 시작**할 수 있다.

---

## 🪐 브라우저 아키텍처

- 브라우저 아키텍처 - 브라우저마다 다름 (표준은 없다)
  - `case 1` 스레드를 많이 사용하는 프로세스 하나만 사용
  - `case 2` 스레드를 조금만 사용하는 프로세스를 여러 개 만들어 IPC로 통신

![https://wd.imgix.net/image/T4FyVKpzu4WKF1kBNvXepbi08t52/BG4tvT7y95iPAelkeadP.png?auto=format&w=845](https://wd.imgix.net/image/T4FyVKpzu4WKF1kBNvXepbi08t52/BG4tvT7y95iPAelkeadP.png?auto=format&w=845)

### 👾 Chrome의 아키텍처

- 다중 프로세스 아키텍처

![https://wd.imgix.net/image/T4FyVKpzu4WKF1kBNvXepbi08t52/JvSL0B5q1DmZAKgRHj42.png?auto=format&w=845](https://wd.imgix.net/image/T4FyVKpzu4WKF1kBNvXepbi08t52/JvSL0B5q1DmZAKgRHj42.png?auto=format&w=845)

![https://wd.imgix.net/image/T4FyVKpzu4WKF1kBNvXepbi08t52/vl5sRzL8pFwlLSN7WW12.png?auto=format&w=845](https://wd.imgix.net/image/T4FyVKpzu4WKF1kBNvXepbi08t52/vl5sRzL8pFwlLSN7WW12.png?auto=format&w=845)

```jsx
⎯ Browser Process : chrome UI영역 기능 - 주소 표시줄, 북마크 막대, 뒤로 가기 버튼, 앞으로 가기 버튼, 네트워크 요청, 파일 접근 등의 권한이 필요한 부분
⎿ Utility Process
⎿ Renderer Process : 웹사이트 렌더링 및 표시 / 각 탭마다 할당(process per tab)
	⎿ 1
	⎿ 2
	⎿ 3
	⎿ ...
⎿ GPU Process : GPU 작업을 별도로 분리
⎿ Plugin Process : 웹사이트 내에서 사용하는 플러그인 제어 (ex. Flash)
⎿ Extension Process : 확장 프로그램 제어
```

- chrome 우측 상단 `점 3개 아이콘` > `도구 더보기` > `작업관리자`  
   → 현재 실행 중인 chrome 프로세스 목록, 사용 중인 CPU와 메모리 양 확인 가능

### 👾 다중 프로세스 아키텍처의 장점

1.  응답 또는 실행이 중단된 프로세스가 일부 발생해도 모든 프로세스가 중단되지 않음

    ⇒ 안정적 & 빠른 사용자 경험

    - 탭마다 할당되는 Renderer Process  
      → 각 탭은 독자적인 프로세스에 의해 실행됨  
      → 한 탭이 응답하지 않으면, 그 탭만 닫고 실행 중인 다른 탭으로 이동 가능.

    - 애플리케이션 내에서 프로세스가 분리되어 있음 (Browser process ≠ Renderer process)  
      → 하나의 탭이 실행 중단되더라도 브라우저 전체의 종료를 막을 수 있으며 오류 페이지를 표시하는 정도로 문제를 처리할 수 있다.

             ❓ 만약 모든 탭이 하나의 프로세스에서 실행된다면?
                 → 탭이 하나만 응답하지 않아도 모든 탭이 응답할 수 없게 됨

1.  보안과 격리
    - 운영체제를 통해 각 프로세스별 권한 제어  
      → 특정 프로세스가 특정 기능을 사용할 수 없도록 제한할 수 있다.

### 👾 다중 프로세스 아키텍처의 단점 : 높은 메모리 사용량

한 애플리케이션 내 서로 다른 프로세스들은 메모리 안에 ‘공통부분’을 가지고 있는 경우가 많다.

    ex. Chrome JavaScript엔진 - V8

하지만 프로세스는 전용 메모리 공간을 갖고, 서로 독립적으로 분리되어 있어 공통 부분에 해당하는 메모리를 공유할 수 없다.

⇒ **메모리 사용량 증가!**

### 👾 Chrome의 메모리 절약 방식

1. 실행 프로세스 개수 제한 (기기 메모리 용량 및 CPU 성능에 따라 다름)

2. 프로세스 개수가 한도를 달성하면, 동일 사이트를 렌더링하는 여러 탭을 하나의 프로세스에서 처리하도록 구현

   ### Chrome의 서비스화

   브라우저의 각 부분을 서비스로 실행해 여러 프로세스로 쉽게 분할 또는 하나로 통합할 수 있도록 아키텍처를 변경하고 있다.

   - 고성능 하드웨어 상에서 실행될 경우 → 각 서비스를 여러 프로세스로 분할해 안정성 ↑
   - 리소스가 제한적인 장치에서 실행될 경우 → 서비스를 하나의 프로세스에서 실행, 메모리 사용량 ↓

---

## 🪐 사이트 격리 (Site Isolation)

프레임별로 실행되는 렌더러 프로세스  
= iframe의 사이트를 별도의 렌더러 프로세스에서 실행

- 격리하는 이유?
  - process per tab 방식 : iframe의 사이트가 동일한 렌더러 프로세스에서 작동. 즉, 서로 다른 사이트 간에 메모리가 공유될 수 있다는 문제점
  - 웹 보안 모델의 핵심인 동일 출처 정책(same origin policy)을 위반
- 사이트 격리 기능의 복잡성
  - 개발자 도구가 자연스럽게 작동할 수 있도록 작업 필요
  - ctrl + F 키로 페이지 내 단어를 검색할 때 : 서로 다른 렌더러 프로세스를 오가며 찾아야 함
