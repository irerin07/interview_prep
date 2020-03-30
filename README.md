# 인터뷰 준비 저장소
인터넷에서 보거나 실제로 받은 면접 질문들을 모아서 공부하고 답변하는 저장소
## 면접 질문
1. 자바
2. 스프링
3. 데이터베이스
4. 기타

### 자바
-  Java 란 무엇인가
    * 운영체제에 종속되지 않고 애플리케이션을 개발할 수 있는 객체 지향적 프로그래밍 언어.
- Java SE와 Java EE 애플리케이션 차이
    * https://www.ibm.com/support/knowledgecenter/ko/SSQP76_8.9.1/com.ibm.odm.dserver.rules.res.managing/topics/con_javase_javaee_applis.html
    * Java Standard Editon
        - 가장 보편적으로 쓰이는 자바 API집합체.
        - 각종 자료구조, 기본 유틸리티, 스윙이나 AWT와 같은 GUI도구등의 기본기능을 포함하고 있다.
    * Java Enterprise Edition
        - 엔터프라이즈 환경을 위한 도구로 EJB, JSP, Servlet, JNDI같은 기능을 지원하며 웹 애플리케이션 서버를 이용하는 프로그램 개발시 많이 사용한다.
- java와 c/c++의 차이점
- java의 접근 제어자의 종류와 특징
    * public - public 접근 제어자가 붙은 변수, 메소드는 어떤 클래스에서도 접근이 가능하다.
    * private - private 접근 제어자가 붙은 변수, 메소드는 자신이 선언 된 클래스에서만 접근이 가능하다. 
    * protected - protected 접근 제어자가 붙은 변수, 메소드는 동일 패키지내의 클래스, 혹은 해당 클래스를 상속받은 외부 패키지의 클래스에서 접근이 가능하다.
    * default - 접근 제어자를 별도로 설정하지 않은 변수 메소드는 자동으로 default 접근 제어자가 붙고, 이들은 자신들이 속한 패키지 내에서만 접근이 가능하다.
    - https://wikidocs.net/232
- OOP의 4가지 특징
    * 추상화 -  공통된 행동(Method)이나 속성(Field)을 모아서 클래스를 만드는 것
    * 캡슐화 - 객체의 행동(Method), 속성(Field)을 하나로 묶고, 실제 구현 내용을 감추는 것.
        * 필드 변수 앞에 접근 제어자 private을 붙인다.
        * 필드 변수에 값을 넣고 가져올 수 있는 메소드를 만든다. (Getter/Setter)
    * 상속 - 상위 객체가 자신이 가지고 있는 필드와 메소드를 하위 객체에게 물려주어 하위 객체가 사용할 수 있도록 하는것
    * 다형성 - 같은 타입이지만 실행 결과가 다양햔 객체를 이용할 수 있는 성질
    - https://github.com/irerin07/java_study#%EA%B0%9D%EC%B2%B4-%EC%A7%80%ED%96%A5-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%EC%9D%98-%ED%8A%B9%EC%A7%95
- OOP의 5대 원칙
    * S - 단일 책임 원칙(SRP, Single Responsibility Principle): 객체는 단 하나의 책임만 가져야 한다.
    * O - 개방-폐쇄 원칙(OCP, Open Closed Principle): 확장에는 열려있어야 하지만 기존 코드의 수정에는 닫혀있어야 한다.
    * L - 리스코프 치환 원칙(LSP, Liskov Substitution Principle): 자식 클래스는 언제나 부모 클래스를 대체할 수 있다.
    * I - 인터페이스 분리 원칙(ISP, Interface Segregation Principle): 인터페이스를 클라이언트에 특화되도록 분리시키라는 설계 원칙이다.
    * D - 의존 역전 원칙(DIP, Dependency Inversion Principle): 의존 관계를 맺을 때 변화하기 쉬운 것 또는 자주 변화하는 것보다는 변화하기 어려운 것, 거의 변화가 없는 것에 의존하라는 것이다.
    * https://irerin07.tistory.com/4
    
- 단일 책임 원칙과 의존 역전 원칙
    *  
    
- 자바는 Call By Value인가 Call By Reference인가
    - 자바는 기본적으로 Call By Value이다.
    - http://mussebio.blogspot.com/2012/05/java-call-by-valuereference.html 
    - https://stackoverflow.com/questions/40480/is-java-pass-by-reference-or-pass-by-value/12429953#12429953
    
- 오버로딩과 오버라이딩의 차이(Overloading vs Overriding)
- String, StringBuilder, StringBuffer
    - String
        - immutable, 불변. 한 번 String Pool 이라는 공간에 생성되면 그 인스턴스의 메모리 공간은 변경될 수 없다.
            - private final char[]의 형태를 가진다.
                - private: 외부에서 접근 불가
                - final: 초기값 변경 불가
        - "+" 혹은 .concat()을 사용하면 새로운 String 인스턴스를 만들고 그 안에 연결 된 문자열을 저장후 참조하게 한다.
        - 문자열을 합치면 기존에 생성되었던 인스턴스는 GC의 대상이 된다. 
            - 각각의 String 주소값이 Stack에 쌓이고, GC가 호출되기 전까지 생성된 String 객체들은 Heap에 쌓이기 때문에 메모리 관리에 치명적이다.
        - 문자열 연산이 적고 참조가 많이 있는 경우 사용하기 좋으며 Thread-safe 하다.
    - StringBuilder
        - mutable, 가변. 연산을 할 때 클래스는 한 번 만들고, 메모리 값을 변경시켜서 문자열을 변경한다.
        - 문자열 연산 등으로 기존 객체에 공간이 부족하게 되는 경우, 기존의 버퍼 크기를 늘리며 유연하게 동작
        - StringBuffer와 StringBuilder 클래스가 제공하는 메서드는 서로 동일
        - 동기화를 보장하지 않음
    - StringBuffer
       - mutable, 가변. 연산을 할 때 클래스는 한 번 만들고, 메모리 값을 변경시켜서 문자열을 변경한다.
       - 문자열 연산 등으로 기존 객체에 공간이 부족하게 되는 경우, 기존의 버퍼 크기를 늘리며 유연하게 동작
       - StringBuffer와 StringBuilder 클래스가 제공하는 메서드는 서로 동일
       - StringBuffer는 각 메서드별로 Synchronized Keyword가 존재하여, 멀티스레드 환경에서도 동기화를 지원
    
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
//물론 생성자 주입과 마찬가지고 전체를 주입할 수도 있다.
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
### 데이터베이스
### 기타