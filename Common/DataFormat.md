# 데이터 교환 형식
---

## JSON
**JSON (JavaScript Object Notation)은 데이터를 교환하는 데 사용되는 경량의 데이터 포맷**

- Javascript 객체문법
- 키(key) : 값(value)으로 구성  
- 이미 존재하는 키를 중복선언하면 나중에 선언한 해당 키에 대응한 값이 덮어쓰이게 됨  
    ```
    a.json
    {
        "name" : "lee"
        "name" : "kim"
        "job" : "developer"
    }

    name == kim
    job == developer
    ```
- 데이터 + 교환 형식
  - 데이터는 추상적인 아이디어에서부터 시작해 구체적인 측정에 이르기까지 다양한 의미로 쓰임
  - 실험, 조사, 관찰 등으로 부터 얻은 사실이나 자료등을 의미
- 여러언어에서의 쓰임
  - javascript -> Object
  - java -> map
  - Python -> dict
  - 해시테이블
- 단순배열, 문자열 표현
    ```
    b.json
    [1, 2, 3, 4]

    c.json
    "가나다라마바사"
    ```
- JSON의 타입
  - javascript object와 유사하지만 undefined, 메서드 등을 포함할 수 없음
  - 수(Number)
  - 문자열(String)
  - 참/거진(Boolean)
  - 배열(Array)
  - 객체(Object)
  - null
- JSON의 활용
  - 프로그래밍 언어와 프레임워크 등에 독립적이므로, 서로 다른 시스템간에 데이터를 교환하기 좋음
  - 주로 API 반환형태, 시스템을 구성하는 설정파일에 활용
  
--- 

## 직렬화 / 역직렬화
**직렬화 : 데이터 구조나 객체 상태를 다른 환경으로 저장하거나 전송할수 있는 형식(문자열/바이트 스트림)으로 변환하는 과정**
- 객체 -> 문자열
- JSON.stringify()

**역직렬화 : 직렬화된 데이터를 원래의 데이터 구조나 객체 상태로 복구하는 과정**
- 문자열 -> 객체
- JSON.parse() 

---

## XML
**XML(Extensible Markup Language)은 마크업 형태 를 쓰는 데이터교환형식**
- 마크업(markup)형태로 태그 등을 이용하여 문서나 데이터의 구조를 나타내는 방법(속성부여도 가능)
- 구성
  - 프롤로그 : 버전, 인코딩
  - 루트요소(단 하나만)
  - 하위 요소들
  ```
  <?xml version="1.0" encoding="UTF-8"?>        // 프롤로그
    <bookstore>                                 // 루트요소
    <book>                                      // 하위 요소
        <title>Learning XML</title>             // 더 작은 요소
        <author>Jane Doe</author>
    </book>
    <book>
        <title>XML Simplified</title>
        <author>John Smith</author>
    </book>
    </bookstore>
  ```
- sitemap.xml
    ```
    <?xml version="1.0" encoding="UTF-8"?>
    <urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9">
        <url>
            <loc>http://www.example.com/foo.html</loc>
            <lastmod>2018-06-04</lastmod>
        </url>
        <url>
            <loc>http://www.example.com/abc.html</loc>
            <lastmod>2018-06-04</lastmod>
        </url>
    </urlset>
    ```
  - 서비스 내의 모든 페이지들을 리스트업한 데이터
  - 사이트가 매우 크거나 서로 링크가 종속적으로 연결되지 않은 경우 크롤러가 일부 페이지를 누락하는 일이 발생, 이를 sitemap.xml이 방지하고 모든 페이지들을 크롤링할 수 있도록 해줌
  - XML은 대표적으로 sitemap.xml에 사용
---

### HTML vs XML
- HTML의 용도는 데이터를 표시 / XML은 데이터를 저장 및 전송
- HTML에는 미리 정의된 태그 사용 / XML에서는 사용자가 고유한 태그를 만들고 정의 가능
- HTML은 대소문자를 구분하지 않음 / XML은 대소문자를 구분

### JSON vs XML
- XML은 닫힌 태그가 존재하기에 JSON보다 무거움
    ```
    JSON
    {
        "bookstore": {
            "book": [
                {
                    "title": "Learning XML",
                    "author": "Jane Doe"
                },
                {
                    "title": "XML Simplified",
                    "author": "John Smith"
                }
            ]
        }
    }


    XML
    <?xml version="1.0" encoding="UTF-8"?>
    <bookstore>
        <book>
            <title>Learning XML</title>
            <author>Jane Doe</author>
        </book>
        <book>
            <title>XML Simplified</title>
            <author>John Smith</author>
        </book>
    </bookstore>
    ```

- Javascript Object로 변환하기 위해 JSON보다 많은 노력이 필요
  - JSON은 JSON.parse()로 끝



> 출처 및 참고 : https://www.inflearn.com/course/%EA%B0%9C%EB%B0%9C%EC%9E%90-%EB%A9%B4%EC%A0%91-cs-%ED%8A%B9%EA%B0%95#