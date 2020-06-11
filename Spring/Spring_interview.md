### 스프링
- 스프링 프레임 워크란
    * IoC와 AOP를 지원하는 경량 컨테이너 프레임워크 
    - POJO 기반의 Enterprise Application 개발을 쉽고 편하게 할 수 있도록 한다.
- IoC란?
    * Inversion of Control(제어의 역전) - 객체 생성을 개발자가 하는것이 아닌 컨테이너가 대신 처리해준다.
- AOP란?
    * Aspect Oriented Programming - 관점 지향 프로그래밍
- Dependency Injection
    * 의존성 주입 - IoC의 형태 중 하나. 클래스 사이에 필요로 하는 의존관계를 컨테이너가 자동으로 처리해주는 것
    
- 스프링 vs 스프링 MVC vs 스프링 부트
    * 스프링은 "IoC와 DI를 지원하는 하나의 거대한 프레임 워크"이며 여러 컴포넌트들을 가진다.
    * 그 컴포넌트중 하나가 바로 스프링 MVC
        * 스프링 MVC는 "Model View Controller 디자인 패턴"을 통해 웹 응용 프로그램을 디자인 할 때 사용
    * 스프링 부트는 Spring 개발을 보다 빠르고 광범위하게 접근 가능하게 만드는 스프링 프레임 워크의 확장도구 같은 것.
        * 스프링 부트의 핵심은 pom.xml(Maven) 혹은 build.gradle(Gradle) 파일 내용에 따라 클래스 패스, 어노테이션, 기타 자바구성클래스를 보고 자동구성하는것
        * 스프링을 쉽게 사용할 수 있도록 필요한 설정을 대부분 미리 세팅 해놓았다는 뜻
        
- What Spring Boot property is used to set the logging level for the entire application in the application.properties file?
    - logging.level.root
- What dependencies does spring-boot-starter-test NOT bring to the classpath?
    - Spring MVC
    - https://mvnrepository.com/artifact/org.springframework.boot/spring-boot-starter-test/2.2.6.RELEASE
- 생성자 주입과 Setter 주입의 차이점
    - http://javainsimpleway.com/setter-dependency-injectionsdi-vs-constructor-dependency-injectioncdi/
    - 생성자 주입과 Setter 주입을 모두 사용하면 스프링 컨테이너는 setter 주입을 우선적으로 사용한다.
    - Partial Dependency 
        * 생성자 주입 방식으로는 Partial Dependency를 구현할 수 없다.
            - 생성자 주입 방식으로는 생성자에 있는 모든 arguments들을 넘겨주어야 하기 때문.
            - 하지만 Setter 방식은 필요한 혹은 원하는 의존성들만 주입하는것이 가능하다.
```
//아래와 같은 코드가 있다고 가정해보자
public class Person {
    private int id;
    private String name;
    private String[] hobbies;
}

public Person(int id, String name, String[] hobbies) {
        this.id = id;
        this.name = name;
        this.hobbies = hobbies;
}
```
```
//생성자 주입을 사용한다면 다음과 같이 주입을 해야 한다.
<bean id="person" class="com.kb.di.Person">
    <constructor-arg value="1" type="int"/>
    <constructor-arg value="Raj"/>
    <constructor-arg>
    <array>
    <value>Playing cricket</value>
    <value>Coding</value>
    <value>Reading books</value>
    </array>
</constructor-arg>
</bean>
```    
```
//만약 아래와 같이 하나라도 빠진다면(지금 같은 경우는 name이 빠진 상태) 에러가 발생한다.
<bean id="person" class="com.kb.di.Person">
    <constructor-arg value="1" type="int"/>
    <constructor-arg>
    <array>
    <value>Playing cricket</value>
    <value>Coding</value>
    <value>Reading books</value>
    </array>
</constructor-arg>
</bean>
```

```
//하지만 setter메소드를 사용한다면
public void setId(int id) {
        this.id = id;
    }
 
    public void setName(String name) {
        this.name = name;
    }
 
    public void setHobbies(String[] hobbies) {
        this.hobbies = hobbies;
    }
```
```
//이와 같이 부분적으로 주입이 가능하다.
<bean id="person" class="com.kb.di.Person">
        <property name="id" value="1"></property>
        <property name="name" value="Raj"></property>
       
</bean>
```
```
//물론 생성자 주입과 마찬가지로 전체를 주입할 수도 있다.
<bean id="person" class="com.kb.di.Person">
        <property name="id" value="1"></property>
        <property name="name" value="Raj"></property>
        <property name="hobbies">
            <array>
                <value>Playing cricket</value>
                <value>Coding</value>
                <value>Reading books</value>
            </array>
 
        </property>
</bean>
```

###쉐어 잇 인터뷰 질문
- 스프링 어노테이션
#### Model View Controller 각 역할
- Model은 어플리케이션이 “무엇”을 할 것인지를 정의 한다. 내부 비지니스 로직을 처리하기 위한 역할을 함.
  - 처리되는 알고리즘, DB, 데이터 등등.
- Controller는 모델이 “어떻게” 처리할 지를 알려주는 역할을 한다.
- View는 화면에 무엇인가를 보여주기 위한 역할을 한다. 컨트롤러 하위에 종속되어, 모델이나 컨트롤러가 보여주려고 하는 모든 필요한 것들을 보여준다. 그리고 사용자의 입력을 받아서 모델의 데이터를 업데이트 한다.
- Controller는 Model과 View가 각각 무엇을 해야 할 지를 알고 있고, 통제한다. 비지니스 로직을 처리하는 Model과 완전히 UI에 의존적인 View가 서로 직접 이야기 할 수 없게 한다.
  
#### 스프링 빈/ 빈 스코프
#### Jpa/ N+1문제
#### 디스패처 서블릿