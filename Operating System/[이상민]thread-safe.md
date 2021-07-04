# Thread-safety

- 스레드의 장점 중 하나는 자원 공유를 통해 낭비를 최소화한다는 점이다
- 하지만 자원 공유로 인해 여러 스레드가 동시에 자원을 사용해 문제가 발생할 수 있다
- 이런 문제를 방지하기 위한게 Thread-safety란 개념이다

# Thread-safe하기 위한 방법들
## 1. immutable 객체를 사용한다
- 값을 변화시키지 않고 읽어 오기만 한다면 immutable한 객체를 사용한다

## 2. synchronized 키워드
- synchronized로 표시된 메소드들은 한번에 하나의 스레드에 의해서만 사용될 수 있다

```java
synchronized void increment() {
    count++;
}
```

## 3. atomic 자료형

- 증감식은 사실 변수 읽어 오기, 1 더하기, 변수에 값 갱신하기 3단계로 나눠서 atomic하지 못하고, 그 때문에 멀티 스레드에서 사용 시 문제가 발생한다
- atomic 자료형에서 제공하는 atomic 메소드들을 통해 문제를 해결할 수 있다 

```java
AtomicInteger count = new AtomicInteger();

void increment() {
    count.incrementAndGet();
}
```

- 다양한 클래스들이 thread-safe를 지원하기 때문에, 문서를 살펴보면 해당 클래스가 thread-safe한지 확인할 수 있다

ex) ConcurrentHashMap, StringBuffer 등