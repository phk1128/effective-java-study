## 🎬 Intro
> item1-생성자 대신 정적 팩터리 메서드를 고려하라

클래스는 인스턴스 반환을 위해 public 생성자 대신 정적 팩터리 메서드를 제공할 수 있다. 이 방식에는 장점과 단점이 모두 존재한다.

## 🎯 정적 팩터리 메서드 장점
### ✅ 이름을 가질 수 있다
#### 생성자 자체만으로는 반환될 객체의 특성을 제대로 설명하지 못한다. 반면 정적 팩터리는 이름만 잘 지으면 반환될 객체의 특성을 쉽게 묘사할 수 있다.

```java
public class Numbers<T extends Number> {
    private final List<T> values;
    
    // 생성자는 순수하게 객체 생성 책임만 담당
    private Numbers(final List<T> values) {
      this.values = values;
    }
    
    // Integer 타입 정적 팩터리 메서드
    public static Numbers<Integer> fromIntegerString(final String inputString) {
      // 유효성 검증 및 파싱
      return new Numbers<>(numbers);
    }

    // Long 타입 정적 팩터리 메서드
    public static Numbers<Long> fromLongString(final String inputString) {
      // 유효성 검증 및 파싱
      return new Numbers<>(numbers);
    }

    // Double 타입 정적 팩터리 메서드
    public static Numbers<Double> fromDoubleString(final String inputString) {
      // 유효성 검증 및 파싱
      return new Numbers<>(numbers);
    }
}
```
- Numbers의 반환되는 제네릭 타입을 메서드 이름을 통해 드러내면, 어떤 타입으로 변환되는지 명확하게 알 수 있음
- 문자열로부터 변환된다는 것도 메서드 이름을 통해 알 수 있음
- 유효성 검증 및 파싱을 정적 팩터리 메서드에서 진행하므로 생성자는 순수하게 객체 생성의 책임만 담당할 수 있음
- 따라서 한 클래스에 시그니처(이름, 매개변수의 타입과 순서)가 같은 생성자가 여러개 필요하다면, 생성자를 정적 팩터리 메서드로 바꾸고 각각의 차이를 잘 드러내는 이름을 지어주자

### ✅ 호출될 때마다 인스턴스를 새로 생성하지 않아도 된다
#### 불변 클래스는 인스턴스를 미리 만들어 놓을 수 있다
```java
public final class Boolean {
    private static final Boolean TRUE = new Boolean(true);   // 미리 생성
    private static final Boolean FALSE = new Boolean(false); // 미리 생성

    private final boolean value;
  
    private Boolean(boolean value) {
      this.value = value;
    }
  
    public static Boolean valueOf(boolean isMatched) {
      // 미리 생성된 인스턴스 반환
      if (isMatched) {
        return TRUE;
      }
        return FALSE;
    }
}
```
#### 새로 생성한 인스턴스를 캐싱하여 재활용할 수 있다(플라이웨이트 패턴)
```java
public class CharacterFlyweight {
    private final char character;
    
    // 캐싱
    private static final Map<Character, CharacterFlyweight> cache = new HashMap<>();
    
    private CharacterFlyweight(char character) {
        this.character = character;
    }
    
    // 플라이웨이트 패턴이 적용된 정적 팩터리 메서드
    public static CharacterFlyweight getInstance(char character) {
        // 캐시에 없으면 새로 생성하고, 있으면 기존 것을 반환
        return cache.computeIfAbsent(character, ch -> new CharacterFlyweight(ch));
    }
    
    public char getCharacter() {
        return character;
    }
}

// 사용 예시
public class ClientExample {
  
  //...
  
    public void check() {
      String text = "Hello";
      List<CharacterFlyweight> characters = new ArrayList<>();

      for (char c : text.toCharArray()) {
        // 같은 문자에 대해서는 동일한 인스턴스를 공유
        characters.add(CharacterFlyweight.getInstance(c));
      }

      // 'l'이 두 번 나오지만, 캐시된 동일한 인스턴스이므로 true
      System.out.println(characters.get(2) == characters.get(3));  // true
  }
}
```
- 위의 2가지 예시 처럼 인스턴스 캐싱하여 재활용하는 식으로 불필요한 객체 생성을 피할 수 있음

### ✅ 반환 타입의 하위 타입 객체를 반환할 수 있다
#### 이를 이용하여 인터페이스를 정적 팩터리 메서드의 반환 타입으로 사용함으로써, 인터페이스 기반 프레임워크를 만들 수 있다. 대표적인 예로 Collections가 있다
```java
// 인터페이스
public interface Collection<E> extends Iterable<E> {
  int size();
  boolean isEmpty();
  //...
}
```

```java
/**
 * 동반 클래스
 * 클래스 이름은 인터페이스의 복수형을 사용하는것이 관례이다
 * 클래스 내부에 package-private(default)로 구현체들이 감춰져있다
 */
public class Collections {

  private Collections() {
  }
  // 정적 팩터리 메서드
  public static <T> List<T> unmodifiableList(List<? extends T> list) {
    if (list.getClass() == UnmodifiableList.class || list.getClass() == UnmodifiableRandomAccessList.class) {
      return (List<T>) list;
    }

    return (list instanceof RandomAccess ?
      new UnmodifiableRandomAccessList<>(list) :
      new UnmodifiableList<>(list));
  }
  
  // package-private(default) 구현체
  static class UnmodifiableList<E> extends UnmodifiableCollection<E> implements List<E> {
    //...
  }
  
  // 정적 팩터리 메서드
  public static <T> List<T> synchronizedList(List<T> list) {
    return (list instanceof RandomAccess ?
      new SynchronizedRandomAccessList<>(list) :
      new SynchronizedList<>(list));
  }

  // package-private(default) 구현체
  static class SynchronizedList<E> extends SynchronizedCollection<E> implements List<E> {
    //...
  }
}
```
- 이처럼 구현체 대부분을 단 하나의 인스턴스화 불가 클래스인 `java.util.Collections`에 감추어져 있다
- 해당 인스턴스들은 정적 팩터리 메서드를 통해서 제공된다

#### 참고
Collections가 여전히 동반 클래스를 사용하는 이유는 다음과 같다.
> - 자바 8부터는 인터페이스가 정적 메서드를 가질 수 있다. 따라서 인스턴스화 불가 동반 클래스를 둘 이유가 별로 없다.
> - 하지만 정적 메서드들을 구현하기 위한 코드 중 많은 부분은 여전히 별도의 package-private 클래스에 두어야 할 수 있다.
> - 자바 8에서도 인터페이스에는 public 정적 멤버만 허용하기 때문이다.
> - 자바 9에서는 private 정적 메서드까지 허락하지만 정적 필드와 정적 멤버 클래스는 여전히 public이어야 한다.

### ✅ 입력 매개변수에 따라 매번 다른 클래스의 객체를 반환할 수 있다

#### 반환 타입을 하위 클래스로 하여 반환 객체를 유연하게 제어할 수 있다

```java
// 추상 게시물 클래스
public abstract class Post {
    protected String content;
    
    // 정적 팩터리 메서드
    public static Post createPost(String type, String content) {
        switch (type) {
            case "text":
                return new TextPost(content);
            case "image":
                return new ImagePost(content);
            case "video":
                return new VideoPost(content);
            default:
                throw new IllegalArgumentException("Unknown post type");
        }
    }
}

// 하위 클래스
class TextPost extends Post {
    public TextPost(String content) {
        this.content = content;
    }
}

class ImagePost extends Post {
    public ImagePost(String content) {
        this.content = content;
    }
}

class VideoPost extends Post {
    public VideoPost(String content) {
        this.content = content;
    }
}
```
- 클라이언트는 구체적인 구현 클래스를 알 필요가 없음
- 새로운 하위 클래스(포스트 타입)을 추가하기 용이함(OCP)
- 상황에 맞는 하위 클래스가 유연하게 반환됨

### ✅ 정적 팩터리 메서드를 작성하는 시점에는 반환할 객체의 클래스가 존재하지 않아도 된다

#### 이러 유연함은 서비스 제공자 프레임워크를 만드는 근간이 된다. 대표적인 서비스 제공자 프레임워크로는 JDBC가 있다

```java
// 서비스 인터페이스
public interface Connection {
   void executeQuery(String query);
   void close();
}

// 서비스 제공자 인터페이스(드라이버 인터페이스)
public interface Driver {
   // 서비스 인터페이스(Connection)의 인스턴스를 생성하는 팩터리 메서드
   Connection connect(String url);
}

// DriverManager - 서비스 접근 API
public class DriverManager {
   // 등록된 드라이버들을 보관
   private static final List<Driver> drivers = new ArrayList<>();
   
   // 드라이버 등록 API
   public static void registerDriver(Driver driver) {
       drivers.add(driver);
   }
   
   // 서비스 접근 API (정적 팩터리 메서드)
   public static Connection getConnection(String url) {
       // 등록된 드라이버들 중에서 URL에 맞는 드라이버를 찾아 연결 생성
       for (Driver driver : drivers) {
           Connection conn = driver.connect(url);
           if (conn != null) {
               return conn;
           }
       }
       throw new RuntimeException("No suitable driver");
   }
}

// MySQL의 Connection 구현체 (나중에 MySQL에서 제공)
public class MySQLConnection implements Connection {
   public MySQLConnection(String url) {
       System.out.println("MySQL DB 연결: " + url);
   }

   @Override
   public void executeQuery(String query) {
       System.out.println("MySQL query 실행: " + query);
   }

   @Override
   public void close() {
       System.out.println("MySQL 연결 종료");
   }
}

// MySQL의 Driver 구현체 (나중에 MySQL에서 제공)
public class MySQLDriver implements Driver {
   // 드라이버 자동 등록(static 초기화 블록)
   // 자바에서 클래스가 로딩 될 때 한 번만 실행되는 특별한 코드 블록
   static {
       DriverManager.registerDriver(new MySQLDriver());
   }

   @Override
   public Connection connect(String url) {
       if (url.startsWith("jdbc:mysql:")) {
           // 서비스 인터페이스(Connection)을 반환
           return new MySQLConnection(url);
       }
       return null; // 처리할 수 없는 URL이면 null 반환
   }
}
```
- 서비스 인터페이스는 구현체의 동작을 정의
- 서비스 제공자 인터페이스가 서비스 인터페이스 인스턴스를 생성하는 팩터리 메서드를 제공, 서비스 제공자 인터페이스가 없으면 각 구현체를 인스턴스로 만들 때 리플렉션을 사용해야 한다.
  ```java
  // 클라이언트 코드 - 리플렉션 사용
  Connection conn = (Connection) Class
      .forName("com.mysql.MySQLConnection")  // 직접 Connection 구현체를 로드
      .getDeclaredConstructor(String.class)  // 생성자를 찾고
      .newInstance("jdbc:mysql://localhost/db");  // 인스턴스 생성
  
  // Oracle로 변경시
  Connection conn = (Connection) Class
      .forName("oracle.jdbc.OracleConnection")
      .getDeclaredConstructor(String.class)
      .newInstance("jdbc:oracle:thin:@localhost:1521:xe");
  ```
- 각 DB 벤더는 Connection과 Driver 인터페이스만 구현하면 됨
- static 초기화 코드 블록으로 인해 자동으로 드라이버 매니저에 등록
- DriverManager.registerDriver가 제공자 등록 API 역할
- DriverManager.getConnection이 서비스 접근 API 역할
    - 클라이언트에게 상황에 맞는 Connection을 유연하게 반환
    - 해당 메서드를 작성하는 시점에는 반환할 객체의 클래스가 존재하지 않아도 됨

```java
// 클라이언트 코드
public class Client {
   public static void main(String[] args) {
       try {
           // 리플렉션을 통해 MySQLDriver클래스의 static 초기화 코드 블록을 실행
           // MySQL 드라이버 로드
           Class.forName("com.mysql.MySQLDriver");
           
           // Connection 획득
           Connection conn = DriverManager.getConnection("jdbc:mysql://localhost/db");
           
           // Connection 사용
           conn.executeQuery("SELECT * FROM users");
           
           // Connection 종료
           conn.close();
           
       } catch (ClassNotFoundException e) {
           System.out.println("드라이버 로드 실패");
       }
   }
}
```
- Class.forName()으로 드라이버 클래스의 static 초기화 코드 블록을 실행(드라이버 로드)
- URL 형식에 따라 적절한 드라이버가 반환 됨
    - `jdbc:mysql:`로 시작하면 MySQL 드라이버가 반환
- 클라이언트는 Connection 인터페이스에만 의존하므로 Oracle, PostgreSQL 등의 새로운 데이터베이스 드라이버로 변경할 때 URL만 변경하면 됨(DIP)

## 🎯 정적 팩터리 메서드 단점
### ✅ 상속을 하려면 public이나 protected 생성자가 필요하니 정적 팩터리 메서드만 제공하면 하위 클래스를 만들 수 없다

#### 상속이 불가능 하므로 확장을 위해서는 컴포지션을 사용한다

```java
// 기본 클래스
public class AudioPlayer {
    private AudioPlayer() {}  // private 생성자
    
    // 정적 팩터리 메서드
    public static AudioPlayer getInstance() {
        return new AudioPlayer();
    }
    
    public void play() {
        System.out.println("음악 재생");
    }
}

// 상속 대신 컴포지션 사용
public class MP3Player {
    private final AudioPlayer audioPlayer;  // AudioPlayer 포함
    private int volume = 5;  // 추가 기능
    
    public MP3Player() {
        this.audioPlayer = AudioPlayer.getInstance();
    }
    
    // AudioPlayer 기능 위임
    public void playMusic() {
        audioPlayer.play();
        System.out.println("현재 볼륨: " + volume);
    }
    
    // 새로운 기능
    public void volumeUp() {
        volume++;
        System.out.println("볼륨 높임: " + volume);
    }
    
    public void volumeDown() {
        volume--;
        System.out.println("볼륨 낮춤: " + volume);
    }
}
```

### ✅ 정적 팩터리 메서드는 프로그래머가 찾기 어렵다
#### 생성자는 JavaDoc에서 Constructors 섹션에 명확하게 표시된다. 반면 정적 팩터리 메서드는 일반 메서드들 사이에 섞여있어 찾기 어렵다

```java
/**
 * Person 클래스는 사람의 기본 정보를 나타냅니다.
 */
public class Person {
    private String name;
    private int age;

    /**
     * 새로운 Person 인스턴스를 생성합니다.
     * @param name 사람의 이름
     * @param age 사람의 나이
     */
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    /**
     * 성인 Person 인스턴스를 생성합니다.
     * @param name 성인의 이름
     * @return 나이가 20세로 설정된 새로운 Person 인스턴스
     */
    public static Person createAdult(String name) {
        return new Person(name, 20);
    }
}
```
```text
Class Person

Constructor Summary
------------------
Person(String name, int age)
    새로운 Person 인스턴스를 생성합니다.

Method Summary
-------------
static Person createAdult(String name)
    성인 Person 인스턴스를 생성합니다.
```

#### 따라서 아래와 같은 네이밍 패턴을 통해 정적 팩터리 메서드임을 명확하게 표현한다

| 네이밍 패턴        | 설명                                          | 예시                                       |
|---------------|---------------------------------------------|------------------------------------------|
| `from`        | 하나의 매개변수를 받아서 해당 타입의 인스턴스를 반환               | `Date.from(instant)`                     |
| `of`          | 여러 매개변수를 받아 인스턴스를 반환                        | `EnumSet.of(JACK, QUEEN, KING)`          |
| `valueOf`     | from과 of의 더 자세한 버전                          | `Boolean.valueOf(true)`                  |
| `getInstance` | 인스턴스를 반환하지만, 같은 인스턴스임을 보장하지 않음              | `Calendar.getInstance()`                 |
| `newInstance` | 새로운 인스턴스 생성을 보장                             | `Array.newInstance(classObject, length)` |
| `getType`     | getInstance와 같으나 다른 클래스에서 팩터리 메서드를 정의할 때 사용 | `Files.getFileStore(path)`               |
| `newType`     | newInstance와 같으나 다른 클래스에서 팩터리 메서드를 정의할 때 사용 | `Files.newBufferedReader(path)`          |
| `type`        | getType과 newType의 간단한 버전                    | `Collections.list(legacyLitany)`         |

## ✨ Summary

### 장점

1. **이름을 가질 수 있다**
- 생성자만으로는 객체의 특성을 제대로 설명하기 어려움
- 정적 팩터리는 이름으로 반환될 객체의 특성을 명확하게 표현

2. **호출마다 새 인스턴스를 만들지 않아도 된다**
- 불변 클래스는 인스턴스를 미리 생성
- 인스턴스 캐싱으로 재활용 가능 (플라이웨이트 패턴)

3. **하위 타입 객체를 반환할 수 있다**
- 유연한 반환 타입 지정 가능
- Collections 프레임워크가 대표적 예시

4. **매개변수에 따라 다른 클래스 객체를 반환할 수 있다**
- 상황에 따른 유연한 객체 생성 가능

5. **정적 팩터리 메서드 작성 시점에 반환할 객체의 클래스가 없어도 된다**
- JDBC가 대표적 예시
- 유연한 서비스 제공자 프레임워크 구현 가능

### 단점

1. **상속이 불가능하다**
- public/protected 생성자가 없으므로 상속 불가
- 대신 컴포지션 사용 권장

2. **프로그래머가 찾기 어렵다**
- JavaDoc에서 생성자처럼 별도 카테고리로 구분되지 않음
- 따라서 명명 규칙을 따르는 것이 중요 (from, of, valueOf 등)

> - 정적 팩터리 메서드와 public 생성자는 각자의 쓰임새가 있으니 상대적인 장단점을 이해하고 사용하는 것이 좋다.
> - 정적 팩터리를 사용하는 게 유리한 경우가 더 많으므로 무작정 public 생성자를 제공하던 습관이 있다면 고치자.
