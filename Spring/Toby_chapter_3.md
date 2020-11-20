#### 토비의 스프링 3장

##### 3.1.1 예외처리 기능을 갖춘 DAO
- 정상적인 JDBC 코드의 흐름을 따르지 않고 중간에 예외가 발생한 경우 사용한 리소스를 반드시 반환해야 한다.
- 아래는 UserDao의 가장 단순한 메소드인 deleteAll() 메소드이다.
```
public void deleteAll() throws SQLException {
    Connection c = dataSource.getConnection();
    
    //아래 두 코드에서 예외가 발생하면 바로 메소드 실행이 중단된다.
    PreparedStatement ps = c.prepareStatement("delete from users");
    ps.excuteUpdate();

    ps.close();
    c.close();
```

- 위에서 두 코드에서 예외가 발생하면 close()메소드가 실행되지 않아 리소스가 반환되지 않을 수 있다.
  - 서버는 제한된 수의 DB커넥션을 만들어 재사용 가능한 풀로 관리한다.
  - DB풀은 매번 getConnection()으로 가져간 커넥션을 명시적으로 close() 해서 돌려줘야 재사용이 가능해진다.
  - 하지만 에러 때문에 제대로 반환이 이루어지지 않으면 풀에 여유가 없어지고 리로스 부족 오류를 내며 서버가 중단될 수 있다.

```
public void deleteAll() throws SQLException {
    Connection c = null;
    PreparedStatement ps = null;
    
    try { // 예외가 발생할 가능성이 있는 코드를 try로 묶는다
        c = dataSource.getConnection();
        ps = c.prepareStatement("delete from users");
        ps.executeUpdate();
    }catch (SQLException e) { //예외가 발생한 경우 부가적인 작업을 해주도록 catch블록을 둔다.
        throw e;
    } finally { //예외가 발생했을때나 안 했을떄 모두 실행되는 finally
        if (ps != null) {
            try {
                ps.close(); // close에서도 예외가 발생할 수 있기 때문에 try-catch로 잡아준다.
            } catch (SQLException e) {
            }
        }
        if (c!= null) {
            try {
                c.close();
            } catch (SQLException e) {
            }
        }
    }
}
```

- 조회를 위한 JDBC코드는 좀 더 복잡하다.
```
public void deleteAll() throws SQLException {
    Connection c = null;
    PreparedStatement ps = null;
    ResultSet rs = null;
    
    try { // 예외가 발생할 가능성이 있는 코드를 try로 묶는다
        c = dataSource.getConnection();
        ps = c.prepareStatement("select count(*) from users");
        rs = ps.executeQuery();
        rs.next();
        return rs.getInt(1);
    }catch (SQLException e) { //예외가 발생한 경우 부가적인 작업을 해주도록 catch블록을 둔다.
        throw e;
    } finally { //예외가 발생했을때나 안 했을떄 모두 실행되는 finally
        if (rs != null) {
            try {
                rs.close(); // close에서도 예외가 발생할 수 있기 때문에 try-catch로 잡아준다.
            } catch (SQLException e) {
            }
        }
        if (ps != null) {
            try {
                ps.close(); // close에서도 예외가 발생할 수 있기 때문에 try-catch로 잡아준다.
            } catch (SQLException e) {
            }
        }
        if (c!= null) {
            try {
                c.close();
            } catch (SQLException e) {
            }
        }
    }
}
```

##### 3.2.1 JDBC try/catch/finally 코드의 문제점
- try/catch/finally가 모든 메소드마다 반복되며 코드가 복잡해졌다.
- 이 문제의 핵심은 변하지 않는, 그러나 많은 곳에서 중복되는 코드와 로직에 따라 자꾸 확장되고 자주 변하는 코드를 분리하는 작업이다.

```
public void deleteAll() throws SQLException {
    Connection c = null;
    PreparedStatement ps = null;
    
    try { 
        c = dataSource.getConnection();
        ps = c.prepareStatement("delete from users"); // 변하는 부분
        ps.executeUpdate();
    }catch (SQLException e) { 
        throw e;
    } finally { 
        if (ps != null) {
            try {
                ps.close(); 
            } catch (SQLException e) {
            }
        }
        if (c!= null) {
            try {
                c.close();
            } catch (SQLException e) {
            }
        }
    }
}
```

- 변하는 부분을 변하지 않는 나머지 코드에서 분리하는 방법
- 메소드 추출
```
private PreparedStatement makeStatement(Connection c) throws SQLException {
    PreparedStatement ps;
    ps = c.prepareStatement("delete from users");
    return ps;
}

public void deleteAll() throws SQLException {
    Connection c = null;
    PreparedStatement ps = null;
    
    try { 
        c = dataSource.getConnection();
        ps = makeStatement(c); -> 변하는 부분만 메소드로 추출
        ps.executeUpdate();
    }catch (SQLException e) { 
        throw e;
    } finally { 
        if (ps != null) {
            try {
                ps.close(); 
            } catch (SQLException e) {
            }
        }
        if (c!= null) {
            try {
                c.close();
            } catch (SQLException e) {
            }
        }
    }
}
```
- 보통 메소드 추출 리팩토링을 적용하는 경우, 분리시킨 메소드를다론 곳에서 재사용할 수 있어야 하는데 위의 코드는 반대로 분리시키고 남은 메소드가 재사용이 필요한 부분이고, 분리된 메소드는 DAO 로직마다 새롭게 만들어서 확장해야 한다.
  - 뭔가 반대로 됐다.

- 템플릿 메소드 패턴 적용
- 상속을 통해 기능을 확장해서 사용하는 부분이다.
  - 변하지 않는 부분은 슈퍼클래스에 두고 변하는 부분은 추상 메소드로 정의해서 서브클래스에서 오버라이드하여 새롭게 정의해 쓰도록 한다.
- 추천해서 별도의 메소드로 독립시킨 makeStatement()메소드를 다음과 같이 추상 메소드 선언으로 변경하고 UserDao역시 추상 클래스로 만든다.
  
```
abstract protected PreparedStatement makeStatement(Connection c) throws SQLException;
```

- 그리고 위의 추상 클래스를 상속하는 서브클래스를 만들어 메소드를 구현한다.

```
public class UserDaoDeleteAll extends UserDao {
    protected PreparedStatement makeStatement(Connection c) throws SQLException {
        PreparedStatement ps = c.prepareStatement("delete from users");
        return ps;
    }
}
```
![tmp](../images/templateMethodpattern.png)
- DAO 로직마다 상속을 통해 새로운 클래스를 만들어야 한다는 점이 큰 단점이다.
- 그림과 같이 UserDao의 JDBC 메소드가 4개라면 그에 맞춰 4개의 서브클래스를 만들어서 사용해야 한다.
- 또한 확장구조가 이미 클래스를 설계하는 시점에서 고정되어 버린다.
  - 변하지 않는 코드를 가진 UserDao의 JDBC try/catch/finally 블록과 변하는 PreparedStatement를 담고 있는 서브클래스들이 이미 클래스 레벨에서 컴파일 시점에 이미 그 관계가 결정되어 있다.
  - 관계에 대한 유연성이 떨어진다.
- 상속을 통애 확장을 하는 템플릿 메소드의 단점이 고스란히 드러난다.

- 전략 패턴의 적용
- 오브젝트를 아예 둘로 분리하고 클래스 레벨에서는 인터페이스를 통해서만 의존하도록 만드는 전략 패턴.
  - 확장에 해당하는 부분인 변하는 부분을 별도의 클래스로 만들어 추상화된 인터페이스를 통해 위임하는 방식.
![sp](../images/strategypattern.PNG)
- deleteAll() 메소드에서 변하지 않는 부분이라고 명시한 것이 contextMethod()가 된다.
- 컨텍스트란 변하지 않는 맥락이다
  - deleteAll()의 컨텍스트
  1. DB커넥션 가져오기
  2. PreparedStatement를 만들어줄 외부 기능 호출
  3. 전달받은 PreparedStatement 실행
  4. 예외 발생시 이를 다시 메소드 밖으로 던지기
  5. 모든 경우에 만들어진 PreparedStatement와 Connection을 적절히 닫기
- PreparedStatement를 만들어주는 외부 기능이 바로 전략 패턴에서의 전략에 해당한다.
- 전략 패턴의 구조를 따라 이 기능을 인터페이스로 만들어두고 인터페이스의 메소드를 통해 PreparedStatement 생성 전략을 호출해주면 된다.
- PreparedStatement를 생성하는 전략 호출시, 해당 컨텍스트 내에서 만들어둔 DB커넥션을 전달해야 한다.
```
package springbook.user.dao;
...
public interface StatementStrategy {
    PreparedStatement makePreparedStatement(Connection c) throws SQLExceptoin ;
}
```
- 위의 인터페이스를 상속해 PreparedStatement를 생성하는 클래스를 생성

```
package springbook.user.dao;
...
public class DeleteAllStatement implements StatementStrategy {
    public PreparedStatement makePreparedStatement(Connection c) throws SQLException {
        PreparedStatement ps = c.prepareStatement("delete from users");
        return ps;
    }
}
```
