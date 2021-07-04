# 멀티스레드 프로그래밍



한 프로세스 내에서 여러 쓰레드로 작업함으로써 CPU 이용률을 높이는 프로그래밍 방법이다.

java.utils.concurrent 패키지에 멀티 쓰레드 프로그래밍을 위한 API들이 준비되어 있다.

Concurrent API는 java 5부터 도입되었지만 점진적으로 업데이트되면서 java8에 이르러 Excecutor, lambda, stream 등이 도입되며

이전까지 프로그래밍하기 어려웠던 멀티스레딩을 쉽게 도입할 수 있게 되었다.



## Executors

자바 8 이전에도 Thread 클래스를 이용해 멀티쓰레드 프로그래밍을 할 수 있었지만 Executors가 도입되면서 더이상 Thread를 사용할 필요가 없어졌다. 스레드를 직접적으로 다루는 가장 최상위 API로 앞으론 Thread 대신 이것을 사용한다. Thread 다음 버전이라 생각하면 된다. Executors는 작업(task)들을 비동기적으로 실행시킬 수 있으며 기본적으로 스레드 풀을 운영한다.



```java
@Slf4j
public class FutureEx {

    public static void main(String[] args) throws ExecutionException, InterruptedException {
        ExecutorService es = Executors.newCachedThreadPool();


        Future<String> future = es.submit(() -> {
            log.info("비동기 작업 start");
            Thread.sleep(3000);
            log.info("Async");
            return "Hello";
        });

        log.info("어떤 오래 걸리는 작업");
        log.info(future.get());
    }
}
```



실행 결과

```
17:46:46.801 [main] INFO FutureEx - 어떤 오래 걸리는 작업
17:46:46.801 [pool-1-thread-1] INFO FutureEx - 비동기 작업 start
17:46:49.810 [pool-1-thread-1] INFO FutureEx - Async
17:46:49.812 [main] INFO FutureEx - Hello
```

다음과 같이 쓰레드 풀에서 쓰레드를 요청한 뒤 병렬 작업을 수행할 수 있다.





# Thread-safe

서로 다른 두 쓰레드간에 경쟁 상태가 발생해도 데이터의 일관성이 깨지지 않도록 설계된 것을 Thread-safe하다고 한다.

기본적으로 멀티스레드 환경의 싱글톤 오브젝트나 여러 스레드가 동시에 접근할 수 있는 오브젝트는 무상태(stateless) 방식으로 만들어야 thread-safe하다.

```java
public class StatefulService {

    private int price; //상태를 유지하는 필드

    public void order(String name, int price) {
        this.price = price; //여기가 문제!
    }

    public int getPrice() {
        return price;
    }
}
```

위 객체를 멀티스레드 환경에서 싱글톤으로 관리할 경우 반드시 문제가 발생한다. 멤버 변수를 가지고 있다면 이는 반드시 final 키워드를 붙여 읽기 전용으로만 사용해야한다.



상태가 없는 방식으로 클래스를 만드는 경우에 각 요청에 대한 정보나, DB, 서버의 리소스 등으로부터 생성한 정보는 어떻게 다뤄야할까? 이때는 파라미터와 로컬 변수, 리턴 값 등을 이용하면 된다. 메서드 파라미터나, 메서드 안에서 생성되는 로컬 변수는 매번 새로운 값을 저장할 독립적인 공간이 만들어지기 때문에 싱글톤이라고 해도 여러 스레드가 변수의 값을 덮어쓸 일은 없다.

*무상태(stateless)*

```java
public class UserDao {

    private SimpleConnectionMaker simpleConnectionMaker;

    public UserDao(SimpleConnectionMaker simpleConnectionMaker) {
        this.simpleConnectionMaker = simpleConnectionMaker;
    }

    public User get(String id) throws SQLException {
        Connection con = simpleConnectionMaker.makeConnection();
        
        ...

        User user = new User();
        user.setId(rs.getString("id"));
        user.setName(rs.getString("name"));
        user.setPassword(rs.getString("password"));
        
        ...

        return user;
    }

}
```



*유상태(stateful)*

```java
public class UserDao {

    private SimpleConnectionMaker simpleConnectionMaker;
    private Connection c;
    private User user;

    public UserDao(SimpleConnectionMaker simpleConnectionMaker) {
        this.simpleConnectionMaker = simpleConnectionMaker;
    }

    public User get(String id) throws SQLException {
        this.c = simpleConnectionMaker.makeConnection();
        
        ...

        this.user = new User();
        this.user.setId(rs.getString("id"));
        this.user.setName(rs.getString("name"));
        this.user.setPassword(rs.getString("password"));
        
        ...

        return user;
    }

}
```

