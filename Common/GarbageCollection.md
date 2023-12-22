# Garbage Collection(GC)란?
프로그램 개발을 하다보면 `유효하지 않은 메모리`인 가비지(Garbage)가 발생하게 됩니다.
그리고 네이티브 언어인 C/C++에서는 개발자가 직접 메모리 관리를 해야했습니다.

C언어에서 간단한 예시를 들면
- malloc() : 특정 크기의 메모리 블록을 동적으로 할당
- free() : malloc(), calloc(). realloc()을 통해 할당된 메모리를 해제

하지만 고수준 언어인 (JAVA, C#, Python 등)에서는 개발자가 직접 메모리 해제를 하지 않고, 가비지 컬렉터가 불필요한 메모리를 알아서 정리해 줍니다.

본문에서는 가장 많이 소개되는 JAVA로 예시를 들겠습니다.

## JAVA에서의 가비지 컬렉션
<img src="https://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/images/gcslides/Slide5.png">

##### 출처 oracle.com
``` 
Permanent Generation은 Java8 이전의 JVM에서 사용되었으며, 지금은 <Metaspace>라는 새로운 메모리 영역으로 대체 되었습니다.
- 클래스와 메소드의 메타데이터 저장
- Java 객체와 클래스 라이브러리 저장
- JVM 외부에서 확장 가능
```
---

Java에서는 JVM(Java Virtual Machine)이 가비지 컬렉션을 관리합니다.
JVM의 힙 영역은 객체들이 할당되는 곳으로, Young영역과 Old영역으로 나뉩니다.

#### Young 영역
- 새롭게 생성된 객체가 할당(Allocation)되는 영역
- 대부분의 객체가 금방 Unreachable 상태가 되기 때문에, 많은 객체가 Young 영역에서 생성되었다가 사라짐
- Young 영역에 대한 가비지 컬렉션을 Minor GC라고 부름

#### Old 영역
- Young 영역에서 Reachable 상태를 유지하며 살아남은 객체가 복사되는 영역
- Young 영역보다 크게 할당되며, 영역의 크기가 큰 만큼 가비지는 적게 발생
- Old영역에 대한 가비지 컬렉션을 Major GC라고 부름

## Young 영역의 구조
Minor GC를 이해하기 전에 Young 영역의 구조에 대한 이해를 해야합니다.
Young 영역은 1개의 Eden 영역과 2개의 Survivor 영역으로 나뉩니다.
- Eden : 새로 생성된 객체가 할당 되는 영역
- Survivor : 최소 1번 이상의 가비지컬렉션 중 살아남은 객체를 보관

## 가비지 컬렉션의 동작 방식

1. Stop The World
    - GC를 수행하기 위해 JVM이 애플리케이션의 실행을 잠시 멈춤
    - STW


| GC종류 | Minor GC | Major GC |
|:---:|:---:|:---:|
| 대상 | Young Generation | Old Generation |
| 실행 시점 | Eden 영역이 꽉 찬 경우 | Old 영역이 꽉 찬 경우 |
| 실행 속도 | 빠르다 | 느리다 |