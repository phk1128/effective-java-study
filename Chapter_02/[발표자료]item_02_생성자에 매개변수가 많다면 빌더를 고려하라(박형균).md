## 🎬 Intro

> item2-생성자에 매개변수가 많다면 빌더를 고려하라

## 🎯 패턴 종류

### ✅ 점층적 생성자 패턴(telescoping constructor pattern)

#### 매개변수를 전부 다 받는 생성자까지 늘려가는 방식

```java
public class NutritionFacts {
  private final int servingSize;
  private final int servings;
  private final int calories;
  private final int fat;
  private final int sodium;
  private final int carbohydrate;

  public NutritionFacts(int servingSize, int servings) {
    this(servingSize, servings, 0);
  }

  public NutritionFacts(int servingSize, int servings,
                        int calories) {
    this(servingSize, servings, calories, 0);
  }

  public NutritionFacts(int servingSize, int servings,
                        int calories, int fat) {
    this(servingSize, servings, calories, fat, 0);
  }

  //...

  public NutritionFacts(int servingSize, int servings,
                        int calories, int fat, int sodium, int carbohydrate) {
    this.servingSize = servingSize;
    this.servings = servings;
    this.calories = calories;
    this.fat = fat;
    this.sodium = sodium;
    this.carbohydrate = carbohydrate;
  }
}
```

다음과 같은 단점이 존재한다

- 매개변수가 많아 질수록 가독성이 떨어짐
- 원치 않는 매개변수까지 값을 지정해줘야 함
- 코드를 읽을 때 각 값의 의미가 무엇인지 헷갈림
- 타입이 같은 매개변수가 연달아 늘어서 있다면, 클라이언트가 실수로 매개변수의 순서를 잘못 건네줘도 컴파일 단계에서 알아채지 못한다

### ✅ 자바빈즈 패턴(JavaBeans pattern)

#### 매개변수가 없는 생성자로 객체를 만든 후, 세터 메서드를 호출해 원하는 매개변수의 값을 설정하는 방식

```java
public class NutritionFacts {
  private int servingSize = -1; // 필수
  private int servings = -1; // 필수
  private int calories = 0;
  private int fat = 0;
  private int sodium = 0;
  private int carbohydrate = 0;

  public NutritionFacts() {
  }

  public void setServingSize(int val) {
    servingSize = val;
  }

  public void setServings(int val) {
    servings = val;
  }

  public void setCalories(int val) {
    calories = val;
  }

  public void setFat(int val) {
    fat = val;
  }

  public void setSodium(int val) {
    sodium = val;
  }

  public void setCarbohydrate(int val) {
    carbohydrate = val;
  }
}
```

점층적 생성자 패턴의 단점들이 자바빈즈 패턴에서는 더 이상 보이지 않는다. 하지만 다음과 같은 단점이 존재한다.

- 객체 하나를 만들려면 메서드를 여러개 호출해야함
- 객체가 완전히 생성되기 전까지는 일관성이 무너진 상태에 놓이게 됨(필수 데이터가 누락된 상태)
- 세터로 인해 클래스를 불변으로 만들 수 없으므로 스레드 안전성이 떨어짐
- freeze 메서드를 통해 불변이 안되는 단점을 보완할 수 있으나, 해당 메서드가 확실히 호출 되었는지 컴파일러가 보증할 방법이 없어서 런타임 오류에 취약하다

```java
public class User {
  private String name;
  private int age;
  private boolean frozen = false; // 객체가 freeze 되었는지 상태를 추적

  // 기본 생성자
  public User() {
  }

  public void setName(String name) {
    checkIfFrozen(); // setter 호출 시마다 freeze 상태 체크
    this.name = name;
  }

  public void setAge(int age) {
    /**
     * checkIfFrozen() 메서드가 누락되어 불변이 아니게 됨
     * 컴파일러는 이를 알아챌 수가 없음
     */
    this.age = age;
  }

  // freeze 메서드 - 객체를 불변 상태로 만듦
  public void freeze() {
    this.frozen = true;
  }

  // freeze 상태 체크 헬퍼 메서드
  private void checkIfFrozen() {
    if (frozen) {
      throw new IllegalStateException("객체가 freeze 되어 수정할 수 없습니다.");
    }
  }
}
```

### ✅ 빌더 패턴(Builder pattern)

#### 필수 매개변수만으로 생성자를 호출해 빌더 객체를 얻고, 빌더 객체가 제공하는 세터 메서드들로 선택 매개변수들을 설정한 뒤, build 메서드를 호출해 최종 객체를 얻는 생성 패턴

```java
public class NutritionFacts {
  private final int servingSize;
  private final int servings;
  private final int calories;
  private final int fat;
  private final int sodium;
  private final int carbohydrate;
  private final List<String> ingredients = new ArrayList<>();

  public static class Builder {
    // 필수 매개변수, 생성자에서 설정 
    private final int servingSize;
    private final int servings;

    // 선택 매개변수, 세터에서 설정  
    private int calories = 0;
    private int fat = 0;
    private int sodium = 0;
    private int carbohydrate = 0;

    public Builder(int servingSize, int servings) {
      // 유효성 검증
      this.servingSize = servingSize;
      this.servings = servings;
    }

    // 세터, this를 리턴하여 메소드 체이닝 형태로 호출 가능
    public Builder calories(int val) {
      // 유효성 검증
      calories = val;
      return this;
    }

    public Builder fat(int val) {
      // 유효성 검증
      fat = val;
      return this;
    }

    public Builder sodium(int val) {
      // 유효성 검증
      sodium = val;
      return this;
    }

    public Builder carbohydrate(int val) {
      // 유효성 검증
      carbohydrate = val;
      return this;
    }

    public Builder ingredients(List<String> val) {
      // 유효성 검증
      // 외부와 참조를 끊어주기 위해 방어적 복사
      this.ingredients = new ArrayList<>(val);
      return this;
    }

    public NutritionFacts build() {
      // 참조 타입이 있다면 방어적 복사를 한 뒤에 유효성 검증
      List<String> ingredientsCopy = new ArrayList<>(ingredients);
      // 유효성 검증

      return new NutritionFacts(this);
    }
  }

  private NutritionFacts(Builder builder) {
    servingSize = builder.servingSize;
    servings = builder.servings;
    calories = builder.calories;
    fat = builder.fat;
    sodium = builder.sodium;
    carbohydrate = builder.carbohydrate;
  }
}
```

```java
NutritionFacts cocaCola = new NutritionFacts.Builder(240, 8)
  .calories(100)
  .sodium(35)
  .carbohydrate(27)
  .build();  
```

다음과 같은 장점이 있다.

- 가독성이 좋음
- 불변이므로 스레드 안정성 보장
- 객체 생성시 일관성 보장

## 🎯 빌더 패턴 장점

### ✅ 빌더 패턴은 계층적으로 설계된 클래스와 함께 쓰기에 좋다

#### 추상 클래스는 추상 빌더를, 구체 클래스는 구체 빌더를 갖게 한다

##### 추상 빌더

```java
public abstract class Pizza {
  public enum Topping {HAM, MUSHROOM, ONION, PEPPER, SAUSAGE}

  final Set<Topping> toppings;

  abstract static class Builder<T extends Builder<T>> {
    EnumSet<Topping> toppings = EnumSet.noneOf(Topping.class);

    public T addTopping(Topping topping) {
      toppings.add(Objects.requireNonNull(topping));
      // return (T) this; 명시적 타입 캐스팅
      return self(); // self() 메서드를 이용하면 명시적인 타입 캐스팅이 필요없다
    }

    abstract Pizza build();

    // 하위 클래스는 이 메서드를 재정의(overriding)하여  
    // "this"를 반환하도록 해야 한다.
    protected abstract T self();
  }

  Pizza(Builder<?> builder) {
    toppings = builder.toppings.clone(); // 아이템 50 참조  
  }
}
```

- Pizza.Builder 클래스는 재귀적 타입 한정을 이용하는 제네릭 타입
    - T는 Builder<T>의 하위 타입
    - Builder<T>에서도 다시 T가 쓰임
    - 이렇게 T의 정의 안에 T자신이 포함되는 구조라서 재귀적이라고 표현
- self() 메서드를 이용하여 하위 클래스에서 형변환하지 않고도 메서드 체이닝을 지원할 수 있음

##### 구체 빌더

```java
public class NyPizza extends Pizza {
  public enum Size {SMALL, MEDIUM, LARGE}

  private final Size size;

  public static class Builder extends Pizza.Builder<Builder> {
    private final Size size;

    public Builder(Size size) {
      this.size = Objects.requireNonNull(size);
    }

    @Override
    public NyPizza build() {
      return new NyPizza(this);
    }

    @Override
    protected Builder self() {
      return this;
    }
  }

  private NyPizza(Builder builder) {
    super(builder);
    size = builder.size;
  }
}
```

- NyPizza.Builder가 상속할 때 그 T자리에 NyPizza.Builder 자신을 타입으로 넣음
- 결과적으로 Pizza.Builder<NyPizza.Builder>를 상속받는 형태가 됨
  ```java
  public static class Builder extends Pizza.Builder<NyPizza.Builder>
  ```
- 따라서 Pizza.Builder의 메서드들이 NyPizza.Builder 타입을 정확하게 다룰 수 있게 됨
  ```java
  NyPizza.Builder builder = new NyPizza.Builder(Size.SMALL);
  // addTopping()은 NyPizza.Builder를 반환하므로
  // 계속 NyPizza의 기능들을 체이닝으로 사용 가능
  builder.addTopping(Topping.SAUSAGE)
        .addTopping(Topping.ONION)
        .build();
  ```

### ✅ 가변인수 매개변수를 여러 개 사용할 수 있다

#### 생성자나 메서드에서는 가변인수 매개변수를 하나만 사용할 수 있다. 하지만 빌더를 사용하면 각각의 세터 메서드가 서로 독립적이므로 여러 개의 가변인수를 받아 객체를 생성할 수 있다

```java
public class Pizza {
  private final Set<String> toppings;
  private final Set<String> sauces;

  public static class Builder {
    private Set<String> toppings = new HashSet<>();
    private Set<String> sauces = new HashSet<>();

    // 가변인수를 사용하는 첫 번째 메서드
    public Builder addToppings(String... toppings) {
      Arrays.stream(toppings).forEach(this.toppings::add);
      return this;
    }

    // 가변인수를 사용하는 두 번째 메서드
    public Builder addSauces(String... sauces) {
      Arrays.stream(sauces).forEach(this.sauces::add);
      return this;
    }

    public Pizza build() {
      return new Pizza(this);
    }
  }
}

// 사용 예시
Pizza pizza = new Pizza.Builder()
  .addToppings("페퍼로니", "올리브", "양파")  // 가변인수 사용
  .addSauces("토마토", "갈릭")               // 다른 가변인수 사용
  .build();

```

- 생성자였다면 이런 방식은 불가능

### ✅ 빌더 하나로 여러 객체를 순회하면서 만들 수 있고, 특정 필드는 빌더가 알아서 채우도록 할 수 있다

```java
public class Order {
  private final int orderId;      // 자동 증가하는 일련번호
  private final String customerName;
  private final List<String> items;

  public static class Builder {
    private static int counter = 1;  // 일련번호를 위한 정적 카운터
    private String customerName;
    private List<String> items = new ArrayList<>();

    public Builder customerName(String name) {
      this.customerName = name;
      return this;
    }

    public Builder addItems(List<String> items) {
      this.items = new ArrayList<>(items);
      return this;
    }

    public Builder reset() {
      customerName = null;
      items.clear();
      return this;
    }

    public Order build() {
      // build 시점에 자동으로 일련번호 할당
      return new Order(counter++, this);
    }
  }

  private Order(int orderId, Builder builder) {
    this.orderId = orderId;
    this.customerName = builder.customerName;
    this.items = builder.items;
  }
}
```

```java
public record OrderData(
  String customerName,
  List<String> items) {
  
}
```

```java
// 주문 데이터
List<OrderData> orderData = Arrays.asList(
    new OrderData("김철수", Arrays.asList("피자", "콜라")),
    new OrderData("이영희", Arrays.asList("치킨", "사이다")),
    new OrderData("박지민", Arrays.asList("햄버거", "감자튀김"))
);

final List<Order> orders = new ArrayList<>();

for (OrderData data : orderData) {
    final Order newOrder = builder.reset() // 빌더 초기화
           .customerName(data.customerName())
           .addItems(data.items())
           .build(); // orderId는 자동으로 할당
    orders.add(newOrder);
}

```

- 하나의 빌더로 데이터를 순회하면서 Order 객체를 생성
- reset()을 통해 새로운 Order 객체 생성가능
- build()를 통해 id를 자동으로 증가시키면서 할당

## 🎯 빌더 패턴 단점

### ✅ 객체를 만들려면, 그에 앞서 빌더 부터 만들어야 한다

#### 빌더 생성 비용이 크지는 않지만 성능에 민감한 상황에서는 문제가 될 수 있다

### ✅ 점층적 생성자 패턴보다는 코드가 장황해서 매개변수가 4개 이상은 되어야 값어치를 한다

#### 하지만 API는 시간이 지날수록 매개변수가 많아지는 경향이 있으므로 단점으로 보기에는 애매하긴 하다

## ✨ Summary

### 점층적 생성자 패턴

- 매개변수를 하나씩 늘려가며 생성자를 만드는 방식
- 단점: 가독성이 떨어지고, 매개변수가 많아지면 관리가 어려움

### 자바빈즈 패턴

- 기본 생성자로 객체를 만들고 setter로 값을 설정
- 단점: 객체 일관성이 깨질 수 있고, 불변 객체를 만들 수 없음

### 빌더 패턴 (권장)

- 필수 매개변수로 빌더 객체를 만들고, 선택 매개변수는 메서드 체이닝으로 설정
- 장점:
    - 가독성이 좋음
    - 불변 객체를 만들 수 있음
    - 계층적 구조에 적합
    - 여러 개의 가변인수 사용 가능
    - 빌더 재사용 가능
- 단점:
    - 객체 생성 전에 빌더부터 만들어야 함 (성능에 민감한 상황에서 문제될 수 있음)
    - 코드가 장황해서 매개변수가 4개 이상은 되어야 값어치를 함

> 생성자나 정적 팩터리 방식으로 시작했다가 나중에 매개변수가 많아지면 빌더 패턴으로 전환할 수도 있지만, 이전에 만들어둔 생성자와 정적 팩터리가 아주 도드라져 보일 것이다.
> 그러니 애초에 빌더로 시작하는 편이 나을 때가 많다.
> - 생성자나 정적 팩터리가 처리해야 할 매개변수가 많다면 빌더 패턴을 선택하는 게 더 낫다. 매개변수 중 닥수가 필수가 아니거나 같은 타입이면 특히 더 그렇다.
> - 빌더는 점층적 생성자보다 가독성이 좋고, 자바빈즈보다 스레드 안전하고 일관성 있는 객체를 생성할 수 있다.
