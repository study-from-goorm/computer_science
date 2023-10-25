# 🌈 좋은 Git Commit message 작성법

## 🌟 Commit message를 규칙에 맞게 작성 해야 할 이유
- #### 더 좋은 commit log 가독성
- #### 더 나은 협업과 리뷰 프로세스
- #### 더 쉬운 코드 유지보수


## 🌟 Commit message 구조

Commit message는 제목, 본문, 꼬리말로 구성
`제목은 필수` 사항이며, 본문과 꼬리말은 선택사항

~~~
<type 타입>: <subject 제목>

<body 본문, 생략가능>

<footer 꼬리말, 생략가능>
~~~


## 🌟 Type의 종류
- #### "type"은 프로젝트나 팀에서 사용하는 규칙이나 관례에 따라 달라집니다. 많은 오픈 소스 프로젝트나 팀들이 특정 커밋 메시지 규칙을 가지고 있으며, 이러한 규칙을 따르는 것이 좋습니다.
- #### 하지만 개인 프로젝트나 정해진 규칙이 없는 프로젝트에서는 원하는 대로 "type"을 정의하고 사용할 수 있습니다.

|키워드|사용시점|
|:---:|:---:|
|feat|새로운 기능 추가|
|fix|버그 수정|
|docs|문서 수정|
|style|코드의 의미에 영향을 주지 않는 변경사항 <br> (코드 포매팅, 세미콜론 누락 등)|
|design|사용자 UI 디자인 변경 (CSS 등)|
|refactor|버그를 수정하거나 기능을 추가하지 않는 코드 변경|
|perf|성능을 향상시키는 코드 변경|
|test|누락된 테스트 추가 또는 기존 테스트 수정|
|chore|빌드 프로세스 또는 보조도구 및 라이프러리 등의 변경|
|ci|CI 관련 설정 수정|
|release|버젼 릴리즈|
|rename|파일 혹은 폴더명을 수정|
|remove|파일을 삭제|

## 🌟 Commit message 7가지 규칙
1. 제목과 본문을 `한 줄` 띄어 `구분`해준다
2. 제목은 `50자 이내`로 작성한다
3. 제목 첫 글자는 `대문자`로 작성한다 (type이 아닙니다)
   - readme file modification ❌
   - Readme file modification ⭕️
4. 제목 끝에 `마침표`를 사용하지 않는다
   - Open the door. ❌
   - Open the door ⭕️
5. 제목은 `명령문`으로, 과거형을 사용하지 않고 `간결`하게 작성한다
   - I fixed the bug ❌
   - Fix the bug ⭕️
6. 본문의 각 `행은 72자 이내`로 작성한다 (줄 바꿈 사용)
7. 본문은 어떻게 보다 `무엇을`, `왜`에 대하여 설명한다
---
<p align="center"><img src="https://blog.kakaocdn.net/dn/cN2ufw/btrueyG3HfY/dNdmtAbvhkg8qko8N0zw0k/img.png" alt="mvc_model1"/></p>