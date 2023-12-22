# 브라우저 렌더링 프로세스

### 브라우저 구성 요소
<p align='center'>
<img src="https://d2.naver.com/content/images/2015/06/helloworld-59361-1.png" width="400" />
</p>

<br/>

### 👾 <u>주소창에 naver.com을 입력하는 순간의 브라우저 동작 과정</u>

> ### 1. DNS Lookup
- naver.com이라는 <u>URL에 해당하는 IP주소를 조회, 변환</u>하는 과정
- 로컬 hosts파일  
→ Local DNS cache  
→ Root DNS 서버 ... 순으로 거슬러 올라가며 도메인에 매칭되는 IP를 조회한다.

<br/>

> ### 2. 서버에 리소스 요청
<p align='center'>
<img src="https://notlaura.com/wp-content/uploads/2018/07/browser-0.svg" width='400'><br/>
</p>

- 통신 element의 네트워크 요청을 통해 서버로부터 리소스를 응답받는다.
- 이 때, 리소스를 **'바이트 스트림'** 형태로 전달받게 된다.
- 브라우저는 DOM Tree를 구축하기 위해 HTML파싱을 진행한다.

<br/>

🌻 Webkit (렌더링 엔진) 동작 과정
<p align="center">
<img src="https://d2.naver.com/content/images/2015/06/helloworld-59361-3.png" width="500">
</p>

> ### 3. HTML파싱 → DOM Tree
<p align='center'>
<img src="https://res.cloudinary.com/practicaldev/image/fetch/s--AQryP0on--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/9h659kk44fxd4ke0soez.png" width="400">
</p>

> 🤖 HTML 파싱 과정  
>    1. [ 바이트 스트림 → 문자 ] 로 디코딩, character화  
>        cf) html `<head>`  
            `<meta charset="utf-8">` : 문서 인코딩 정보
>    2. **토큰화(Tokenization)**  
        : 디코딩한 문자열을 하나씩 읽어나가며 어휘를 분석한다. 시작 태그, 종료 태그, 속성 이름, 속성 값 등을을 해석한 결과 HTML 토큰이 생성된다.
>    3. **Node 생성** : 토큰을 **O**jbect화 함으로써 의미 있는 단위로 재해석한다.  
        ```
        {
            tag: div,
            attribute: ...
        }
        ```  
>    4. **DOM Tree** 생성 : 각 노드 간 관계성을 부여해 트리를 생성한다.  
<p align="center">
<img src="https://d2.naver.com/content/images/2015/06/helloworld-59361-8.png" width="300">
</p>

<br/>

> ### 4. Style Sheet 파싱 → CSSOM Tree
```
    <head>
        ...
        <link rel="stylesheet" href="style.css">
        ...
    </head>
```
- HTML 파일에서 css파일이 명시된 `link` 태그를 만나는 순간, 해당 파일에 대해 서버에 재요청을 보내고 css 파일을 전달받는다.
- DOM Tree 생성 과정과 동일하게 CSSOM Tree를 파싱해 스타일 규칙을 얻는다.  
    : 바이트 스트림 → 캐릭터화 → 토큰화 → 노드 생성 → CSSOM Tree 생성  
<p align="center">
<img src="https://d2.naver.com/content/images/2015/06/helloworld-59361-12.png" width="400">
</p>

<br/>

> ### 5. script와 stylesheet의 진행
- 기본 원리 : 브라우저는 HTML을 파싱하여 DOM을 생성함과 동시에 즉시 이를 실행한다.
> #### 🌻 script 파일
- HTML 파싱 도중 script태그를 만날 경우, 해당 JavaScript 파일을 요청하고, 응답받은 파일을 즉시 실행하게 된다.  
- <u>script파일이 실행되는 동안 HTML파싱은 중단되며,</u> 완료된 후 파싱을 재개한다.  
- 이 특성 때문에 주로 \<script> tag는 html body의 최하단에 삽입한다.
- cf) HTML5 - defer, async : \<script>가 상단에 있어도 DOM의 생성을 막지 않게 하는 속성
> #### 🌻 stylesheet 파일
- JavaScript와 달리 CSS는 DOM의 생성을 막지 않는다. → 태그가 상단에 위치할 수 있는 이유
- 단, DOM과 CSSOM이 모두 완성되어야만 다음 단계인 Render Tree 생성을 진행할 수 있기 때문에, CSSOM을 최대한 빠르게 완성하는 것이 브라우저 성능에 있어 중요한 요인으로 작용한다.  

<br/>

> ### 6. Render Tree 생성

<p align="center">
<img src="https://res.cloudinary.com/practicaldev/image/fetch/s--GvgtxfN---/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/8l7o8i1bsy78h67kud7c.png">
</p>

- 파싱 단계에서 구축된 DOM, CSSOM Tree는 Render Tree로 결합된다.
- 각각의 DOM node는 `attach`라는 메소드를 가지는데, 새로운 DOM node가 추가될 때마다 attach가 호출되며 즉시 Render Object를 생성하게 된다.
    ```
        렌더링 과정을

            1. DOM Tree 구축
            2. Render Tree 구축
            3. Render Tree 배치
            4. Render Tree 그리기

        로 나눈다면, 이 때 1번과 2~4번이 '병렬적으로' 진행된다.

        모든 DOM Tree 요소가 파싱될 때까지 기다리는 것이 아니라, 
        개별 DOM 노드들이 생성되자마자 각각 Render Object 생성, 배치 과정을 거쳐 그려지게 된다.
    ```
- `head`, `meta`, `display=none` 속성을 가진 tag 등은 화면 렌더링 시 불필요한 요소  
→ Render Object로 생성되지 않고, Render Tree에서 제외된다.

<br/>

> ### 7. Layout (Reflow)
- 렌더 트리의 각 노드를 뷰포트에 배치하기 위해 해당 요소의 정확한 위치 및 크기를 계산하는 작업
- 렌더링 과정에서 한 번만 발생하지 않으며, 아래의 경우에 요소 위치가 다시 계산된다.
    - DOM에서 요소가 추가 혹은 삭제되는 경우
    - 브라우저의 창 크기를 조정하는 경우 (Viewport 크기 변경)
    - 요소의 너비, 위치, 크기 등이 변경되는 경우
    - 폰트 및 이미지 크기 등이 변경되는 경우


<br/>

> ### 8. Paint
- Layout 단계에 의해 배치가 완료된 Render Tree를 픽셀로 화면 상에 그리는 단계
- Render Tree 탐색 후 각 Render Object의 `paint` 메소드를 호출한다.
- 아래의 상황일 경우 Paint 과정이 여러 번 발생하게 된다.
    - 요소 Outline 변경
    - background color 변경
    - 불투명도, 가시성 변경
- 한 페이지에 모든 요소를 그리는 것이 아닌, 화면을 여러 개의 레이어로 나눠서 Paint한다.

<br/>

> ### 9. Composite
- Paint한 여러 겹의 레이어들을 하나로 합치는 단계

<br/>

#### Layout ~ Composite 단계는 최초 렌더링 이후에도 반복된다.




---
### 참고
https://d2.naver.com/helloworld/59361  
https://davidhwang.netlify.app/Developments/browser-rendering-process/  
https://dev.to/arikaturika/how-web-browsers-work-parsing-the-html-part-3-with-illustrations-45fi  
https://youtu.be/Mqh13dNI8jc?si=d94XT1zOCkypf8yR  