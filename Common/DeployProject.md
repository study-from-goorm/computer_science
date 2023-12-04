## 🗃️ 배포 준비: 프로덕션 환경을 위한 빌드 프로세스
</br>

---

</br>

## React 앱 빌드
- **목적** : 프로덕션 환경에 배포하기 위해 React 앱을 최적화하고, 모든 필요한 파일을 하나의 디렉토리에 모으는 것
- **방법** :
  - 이 명령은 코드를 최소화(minification)하고, 모든 정적 파일을 build 디렉토리에 모음
```
npm run build # or yarn build
```  
- **주의사항** :
    - 환경 변수 (예: API 엔드포인트)는 프로덕션 환경에 맞게 설정해야 함
    
</br>
</br>

## Java Spring Boot 앱 패키징
- **목적** : Spring Boot 앱을 자가 실행 가능한 JAR 또는 WAR 파일로 패키징하여 배포 준비
- **방법** :
  - 패키징 과정에서 필요한 모든 의존성을 포함하는 실행 가능한 JAR 파일이 생성
```
mvn package # Maven 사용 시
gradle build # Gradle 사용 시
```
- **주의사항** :
    - 프로덕션 환경에 맞는 데이터베이스 설정, 포트 설정 등의 환경 설정이 필요

</br>

---
</br>

## 배포 지원 도구 : AWS, Heroku, Docker
</br>

<img src="https://velog.velcdn.com/images/k-minsik/post/797c5519-57db-44d0-b8b3-12a7363011ce/image.png" width="30%" height="30%">

#### AWS (Amazon Web Services)
배포를 위한 공간만 대여, 프로젝트에 관한 모든 셋팅을 직접 해야함 -> IaaS
- **장점** :
    - 높은 확장성과 유연성
    - EC2, S3, RDS 등 다양한 서비스 제공
    - 비용이 저렴
- **단점** :
    - 설정과 관리가 복잡함

</br>
</br>
</br>

<img src="https://velog.velcdn.com/images/k-minsik/post/9d8c3e79-b493-416b-981b-76b8db156047/image.webp" width="40%" height="40%">

#### Heroku
완성형 서버 배포 플랫폼, 코드만 있다면 도메인(URL)과 기타 자원들을 제공 -> Paas
- **장점** :
    - 사용이 간편하고 빠른 배포 가능
    - 무료 티어 제공
- **단점** :
    - 확장성과 커스터마이징에 제한 (패키지 버젼 ...)
    - 비용이 비쌈

</br>
</br></br>

<img src="https://velog.velcdn.com/images/k-minsik/post/cdbaf062-96e2-4107-a2a8-6132281e907e/image.png" width="30%" height="30%">

#### Docker
소프트웨어 컨테이너화 플랫폼, 어떤 환경이든 일관된 동작을 보장, 클라우드 서비스 모델보다는 개발 및 배포의 효율성을 높이는 기술
- **장점** :
    - 환경 일관성 보장
    - 여러 환경에서 쉽게 배포 가능
- **단점** :
    - 컨테이너 관리에 대한 추가 지식 필요
    - 보안 설정에 주의 필요

</br>

--- 
</br>

## CI/CD 파이프라인: Jenkins, GitHub Actions
> CI/CD (Continuous Integration, 지속 통합 / Continuous Deployment, 지속배포)


<img src="https://velog.velcdn.com/images/k-minsik/post/280ee8ed-70a6-4ef9-87ee-c2997aca31f4/image.png" width="30%" height="30%">

#### Jenkins
Java로 작성된 오픈소스 자동화 서버이며, CI/CD 파이프라인을 구축하는 데 널리 사용
- **장점** :
    - 강력한 자동화와 커스터마이징 가능
    - 다양한 플러그인 제공
- **단점**:
    - 설정과 관리가 복잡함
    - 초기 설정에 시간 소요

</br>
</br>
</br>

<img src="https://velog.velcdn.com/images/k-minsik/post/de66fd8c-2836-48ae-b7ed-bc6b1b536e2f/image.png" width="40%" height="40%">

#### GitHub Actions
 GitHub의 CI/CD 플랫폼으로, GitHub 저장소를 기반으로 소프트웨어 개발 워크플로우를 자동화
- **장점** :
    - GitHub 저장소와 통합 용이함
    - 간단하고 빠른 설정
- **단점** :
    - 복잡한 워크플로우에 한계
    - Jenkins에 비해 대규모 시스템에서 제한적