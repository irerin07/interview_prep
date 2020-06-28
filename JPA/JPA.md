#### JPA
##### JAVA PERSISTENCE API
- 자바 진영의 ORM 표쥰 기술

#### ORM
##### Object Relational MApping
- 객체는 객체대로, 관계형 DB는 관계형 DB대로 설계
- ORM 프레임워크가 중간에서 Mapping해준다.

##### JPA는  JAVA Application과 JDBC 사이에서 동작한다.
### 가장 핵심적인 부분은 바로 패러다임 불일치를 해결해준다는것.

#### JPA 사용 이유
- 생산성 증가.
    - CRUD가 편하다.
    - 유지보수가 편하다.
        - 기존: 필드 변경시 모든 SQL을 수정해야 했다.
        - JPA: 필드만 추가 해주면 알아서 해결 해준다.
    - 패러다임 불일치 해결
    - JPA를 통한 자유로운 객체 그래프 탐색
    - 동일한 트랜잭션에서 조회한 Entity는 같음을 보장한다.