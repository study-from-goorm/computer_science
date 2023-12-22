# 가비지 컬렉션(GC)이란? 🚮

프로그램 개발을 하다 보면 `유효하지 않은 메모리`인 가비지(Garbage)가 발생하게 됩니다. 네이티브 언어인 C/C++에서는 개발자가 직접 메모리 관리를 해야 했습니다.

C언어에서의 간단한 예시:
- `malloc()` 🧱: 특정 크기의 메모리 블록을 동적으로 할당
- `free()` 🧹: `malloc()`, `calloc()`, `realloc()`을 통해 할당된 메모리를 해제

하지만 고수준 언어인 (JAVA, C#, Python 등)에서는 개발자가 직접 메모리를 해제하지 않고, 가비지 컬렉터가 불필요한 메모리를 알아서 정리해 줍니다.

본문에서는 가장 많이 소개되는 JAVA로 예시를 들겠습니다.

## JAVA에서의 가비지 컬렉션 🌿


<img src="https://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/images/gcslides/Slide5.png">


##### 출처: oracle.com

```
Permanent Generation은 Java8 이전의 JVM에서 사용되었으며, 지금은 <Metaspace>라는 새로운 메모리 영역으로 대체되었습니다. (8부터는 Native Method Stack에 편입)
```
---

Java에서는 JVM(Java Virtual Machine)이 가비지 컬렉션을 관리합니다. JVM의 힙 영역은 객체들이 할당되는 곳으로, Young 영역과 Old 영역으로 나뉩니다.
- **Reachable**: 객체가 참조되고 있는 상태
- **Unreachable**: 객체가 참조되고 있지 않은 상태 (GC의 대상이 됨)

Java에서는 참조되지 않고 있는 상태의 객체를 제거하여 가비지 컬렉션을 진행합니다.

#### Young 영역 🌱
- 새롭게 생성된 객체가 할당(Allocation)되는 영역
- 대부분의 객체가 금방 Unreachable 상태가 되기 때문에, 많은 객체가 Young 영역에서 생성되었다가 사라짐
- Young 영역에 대한 가비지 컬렉션을 Minor GC라고 부름

#### Old 영역 🌳
- Young 영역에서 Reachable 상태를 유지하며 살아남은 객체가 복사되는 영역
- Young 영역보다 크게 할당되며, 영역의 크기가 큰 만큼 가비지는 적게 발생
- Old 영역에 대한 가비지 컬렉션을 Major GC라고 부름

## Young 영역의 구조 🔍
Minor GC를 이해하기 전에 Young 영역의 구조에 대한 이해가 필요합니다.
Young 영역은 1개의 Eden 영역과 2개의 Survivor 영역으로 나뉩니다.
- **Eden**: 새로 생성된 객체가 할당되는 영역
- **Survivor**: 최소 1번 이상의 가비지컬렉션 중 살아남은 객체를 보관

## 가비지 컬렉션의 동작 방식 🔄

1. **Stop The World** 🛑
    - GC를 수행하기 위해 JVM이 애플리케이션의 실행을 잠시 멈춤
    - STW(Stop The World)라고도 불림
2. **Mark and Sweep** 🖊🧹
    - **Mark**: 사용 중인 메모리와 사용되지 않는 메모리 식별
        - Root Space로부터 그래프 순회를 통해 연결된 객체를 찾아내어 각각 어떤 객체를 참조하고 있는지 찾아서 마킹
    - **Sweep**: 사용되지 않는 메모리를 해제
        - 참조하고 있지 않은 객체를 Heap에서 제거

## Minor GC 🚀

Young 영역에서 발생하며, 새로 생성된 객체 중 더 이상 필요 없게 된 객체를 제거합니다.

1. 새로 생성된 객체가 Eden 영역에 할당된다.
2. 객체가 계속 생성되어 Eden 영역이 꽉차게 되고 Minor GC가 실행된다.
3. Eden 영역에서 사용되지 않는 객체의 메모리가 해제된다.
4. Eden 영역에서 살아남은 객체는 1개의 Survivor 영역으로 이동된다.

1~2번의 과정이 반복되다가 Survivor 영역이 가득 차게 되면 Survivor 영역의 살아남은 객체를 다른 Survivor 영역으로 이동시킵니다.(1개의 Survivor 영역은 반드시 빈 상태가 된다.)
이러한 과정을 반복하여 계속해서 살아남은 객체는 Old 영역으로 이동(Promotion)됩니다.

## Major GC 🌪

Old 영역에서 발생하며, 시간이 오래된 객체 중 더 이상 필요 없게 된 객체를 제거합니다. Major GC는 일반적으로 Minor GC보다 더 오래 걸리고, 애플리케이션에 더 큰 영향을 줄 수 있습니다.

## Full GC 🌝

JVM의 모든 영역 (Young Generation, Old Generation 및 Permanent/Metaspace 영역)에서 발생하는 가비지 컬렉션을 말합니다.
Full GC는 모든 객체를 검사하고 정리하기 때문에 가장 많은 시간을 소비하며, 애플리케이션에 가장 큰 영향을 줄 수 있습니다.
일반적으로 Full GC는 시스템 메모리가 매우 부족할 때 발생하며, Old Generation이나 다른 메모리 영역의 가비지 컬렉션이 충분하지 않을 때 발생할 수 있습니다.

## 정리 📝

1. **실제 면접에서 가비지 컬렉션에 대한 질문**: APM(Application Performance Management)서비스와 연관지어 풀어나가는 것이 좋다고 합니다. (Garbage Collection에 대한 지식
뿐만 아니라, 배포 유지보수 했을 때 적용하는 방법에 대한 질문 일 수 있음)

2. **Stop The World 이벤트**: 성능에 영향을 주며, 어플리케이션의 사용성을 유지하면서 효율적으로 GC를 실행하는 최적화 작업이 개발자의 숙제라고 할 수 있습니다. 이러한 GC 최적화 작업을 GC 튜닝이라고 합니다. (예: Serial GC, Parallel GC 등)

## 한눈에 보기 👀

| GC종류 | Minor GC | Major GC |
|:---:|:---:|:---:|
| 대상| Young Generation | Old Generation |
| 실행 시점 | Eden 영역이 꽉 찬 경우 | Old 영역이 꽉 찬 경우 |
| 실행 속도 | 빠르다 | 느리다 |

```
참고자료 : https://mangkyu.tistory.com/118

참고유튜브 : https://youtu.be/24f2-eJAeII?si=UcDCpXkii4eJvjjQ
```
