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
    
- 단일 책임 원칙 vs 의존 역전 원칙
    * 
### 스프링
### 데이터베이스
### 기타