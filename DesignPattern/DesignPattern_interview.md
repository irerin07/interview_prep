### 디자인 패턴
![joins](../images/gof_types.png)
#### Singleton 패턴
- Creational Pattern, 생성 패턴
- 인스턴스가 하나뿐인 특별한 객체를 만들 수 있게 해주는 디자인 패턴
- 생성자가 private으로 지정되어있다.
- 즉 인스턴스를 직접 만드는것이 아니라 인스턴스를 "달라고 요청"하는 것
- 문제점
    - 단일 스레드라면 문제가 없겠지만 스레드가 여러개인 경우(멀티 스레드) 의도치 않게 여러개의 객체가 만들어질 수 있다.
- 해결방법
    - 인스턴스를 반환하는 메서드를 동기화(synchronized) 시키면 간단하게 해결할 수 있다.
    - 하지만 동기화가 꼭 필요한 시점은 해당 메서드가 시작되는 순간 뿐이다.
- 효율적인 해결방법
    1. 인스턴스를 필요할 때 생성하는 것이 아닌, 처음부터 만들어 버린다.(static)
        - static을 사용하면 클래스가 로딩될 때 JVM에서 Singleton의 유일한 인스턴스를 생성해준다.
    2. Double Checking Locking (DCL)을 사용해 동기화되는 부분을 줄인다.
        - DCL을 사용하면 일단 인스턴스가 생성되어 있는지 확인한 다음, 생성되어 있지 않은 경우에만 동기화를 할 수 있다.
        - 다만 DCL은 자바 1.5버전 부터 사용할 수 있다.
- 스프링은 기본적으로 별다른 설정을 하지 않으면 내부에서 생성하는 빈 오브젝트를 모두 싱글톤으로 만든다.
    - 엄밀히 말하자면 스프링은 직접 싱글톤 형태의 오브젝트를 만들고 관리하는 기능을 제공한다. -> 싱글톤 레지스트리
    - [출처](http://blog.naver.com/PostView.nhn?blogId=kjy6268&logNo=50107958407)

```java
public class singleton {
    private volatile static Singleton uniqueInstance; 
    // volatile 키워드를 사용하면 멀티스레딩을 쓰더라도 
    // uniqueInstance변수가 Singleton 인스턴스를 초기화 되는 과정이 
    // 올바르게 진행되도록 할 수 있다.
    private Singleton() {}
    public static Singleton getUniqueInstance() {
        if(uniqueInstance == null){
            synchronized (Singleton.class) {
                if (uniqueInstance == null) {
                    uniqueInstance = new Singleton();
                }
            }
        }
        return uniqueInstance;
    }
}
```