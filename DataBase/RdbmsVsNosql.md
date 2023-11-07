## RDBMS vs NoSQL 🌐

데이터베이스의 세계는 항상 발전하고 있습니다. 초기 데이터 관리 시스템에서부터 지금까지, 데이터의 중요성이 늘어나면서 그 저장과 검색 방법도 다양해졌습니다. 관계형 데이터베이스(RDBMS)는 오랜 시간 동안 업계의 표준으로 사용되어왔지만, 스케일과 다양한 데이터 형식의 필요성이 높아지면서 NoSQL이 대안으로 떠오르게 되었습니다.

이제 둘 사이의 주요 차이점을 표와 함께 간략하게 살펴보겠습니다.

---

### 1️⃣ 대표적인 예시 📖

- **RDBMS**: MySQL, Oracle, Microsoft SQL Server(Ms SQL)
- **NoSQL**: MongoDB[* JS], Cassandra[* CQL], Redis[* 명령어 기반], Couchbase[* N1QL]

---

### 2️⃣ RDBMS와 NoSQL 간단 비교 📊

| 항목   | RDBMS     | NoSQL     |
|-------|--------|--------|
| 데이터 구조    | 테이블과 관계   | 문서, 키-값, 그래프, 컬럼 기반 등 다양함  |
| 스키마     | 고정적 (강한 스키마) | 유연함 (자유로운 스키마)     |
| `확장성`     | 수직 확장       | `수평 확장`      |
| 트랜잭션   | ACID(안정성과 무결성 보장을 위한 속성)를 지원   | 대부분은 ACID를 지원하지 않음   |
| 쿼리 언어        | SQL        | 데이터베이스마다 다름     |
| Join연산  | O  | 제한적 지원 |
| 용어/ 개념 | 테이블, 로우, 컬럼 | 컬렉션, 다큐먼츠, 컬렉션 |
| 사용예시 분야  | 쇼핑몰   | FaceBook, Instagram (대규모 분석)   |

---

### 3️⃣ 실행 화면

### ✨ RDBMS (예: MySQL)

데이터베이스와 테이블 생성 (DDL) :
```sql
CREATE DATABASE Company;
USE Company;

CREATE TABLE Employees (
    ID INT PRIMARY KEY,
    Name VARCHAR(50),
    Position VARCHAR(50),
    Age INT
);
```

데이터 추가 (DML) :
```sql
INSERT INTO Employees (ID, Name, Position, Age)
VALUES (1, 'John Doe', 'Manager', 32);
```

데이터 조회 (DML):
```sql
SELECT * FROM Employees WHERE Age > 30;
```

결과:
```
+----+---------+---------+-----+
| ID |  Name   | Position| Age |
+----+---------+---------+-----+
|  1 | John Doe| Manager | 32  |
+----+---------+---------+-----+
```

---

### ⚡️ NoSQL (예: MongoDB)

데이터베이스와 컬렉션 생성:
```javascript
use Company
```

데이터 추가:
```javascript
db.employees.insert({
    "ID": 1,
    "Name": "John Doe",
    "Position": "Manager",
    "Age": 32
});
```

데이터 조회:
```javascript
db.employees.find({ "Age": { "$gt": 30 } });
```

결과:
```javascript
{
    "_id": ObjectId("5f4d7f82e98f8f7f28d89767"),
    "ID": 1,
    "Name": "John Doe",
    "Position": "Manager",
    "Age": 32
}
```

위의 예시는 RDBMS와 NoSQL의 간단한 실행화면을 텍스트로 표현한 것입니다. 실제 환경에서는 GUI 기반의 관리 도구(예: MySQL Workbench, MongoDB Compass) 또는 커맨드라인 인터페이스를 사용하여 실행할 수 있습니다.

---

### 🌈 마치며... 

쉬운 이해를 위해 필자는 RDBMS를 `보수적 성향의 시스템` NoSQL을 `진보적 성향의 시스템` 이라고 이해했습니다.
하지만 이것은 단편화된 비유이므로 실제로는 더욱 구체적으로 고려해야 합니다!

정리하자면 데이터 무결성이 중요한 경우에는 RDBMS를, 높은 확장성과 유연성이 필요한 경우에는 NoSQL을 선택하는 것이 중요합니다.

---
### 💡 주요단어
```
* 수평 확장(Horizontal Scaling): 기존의 서버나 노드에 추가적인 서버나 노드를 더하는 방식으로 시스템의 용량을 확장하는 것을 말합니다. 이를 "스케일 아웃(Scale Out)"이라고도 합니다.

* 수직 확장(Vertical Scaling): 기존의 서버나 노드의 하드웨어 성능(예: CPU, RAM)을 향상시켜 시스템의 용량을 확장하는 것을 말합니다. 이를 "스케일 업(Scale Up)"이라고도 합니다.

* DDL (데이터 정의어) : 데이터베이스를 정의하는 언어를 말하며 데이터를 생성하거나 수정, 삭제 등 데터의 전체 골격을 결정하는 역할의 언어를 말한다.

* DCL (데이터 제어어) : 데이터베이스에 접근하거나 객ㅔ에 권한을 주는 등의 역할을 하는 언어를 말한다.

* DML (데이터 조작어) : 정의된 데이터베이스에 입력된 레코드를 조회하거나 수정하거나 삭제하는 등의 역할을 하는 언어를 말한다.
```