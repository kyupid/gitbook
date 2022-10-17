# 이펙티브 자바

## 2장 객체 생성과 파괴

### 아이템1 생성자 대신 정적 팩터리 메서드를 고려하라

클래스의 인스턴스를 얻는 가장 기본적인 방식은 public 생성자이다.

public 생성자 대신에 정적 팩터리 메서드를 고려하라.

#### 정적 팩터리 메서드의 장점은 무엇일까?

1. **이름을 가질 수 있다.** `BigInteger(int, int, Random)` 보다는 `BigInteger.probablePrime` 이 생성하는 행위의 역할을 더 잘 나타낸다.
2. **호출될 때마다 인스턴스를 새로 생성하지 않아도 된다.**\
   반복되는 요청에 같은 객체를 반환하는 식인 정적 팩터리 메서드의 클래스는 언제 어느 인스턴스를 살아 있게 할 것인지 철저히 통제할 수 있다.\
   인스턴스를 통제하면, 클래스를 싱글턴 또는 인스턴스화 불가로 만들 수 있다.\
   또한 불변값 클래스에서 동치인 인스턴스가 단 하나뿐임을 보장 할 수 있다
3. **반환 타입의 하위 타입 객체를 반환할 수 있는 능력이 있다.**\
   ****_Q) 동반 클래스란?, TODO) 해당 부분 다시 이해 필요_
4. **입력 매개변수에 다라 매번 다른 클래스의 객체를 반환할 수 있다**
5. **정적 팩터리 메서드를 작서하는 시점에는 반환할 객체의 클래스가 존재하지 않아도 된다.**

### 아이템2 생성자에 매개변수가 많다면 빌더를 고려하라

생성자에 매개변수가 많으면 각 매개변수들의 의미파악도 힘들고 매개변수의 순서나 갯수까지 파악해야하는 수고를 들여야한다.  대안으로 자바빈즈 패턴을 사용할 수 있다. 자바빈즈패턴은 매개변수없이 인스턴스를 생성하고 setter 로 인스턴스를 완성시키는 것이다. 자바빈즈패턴의 문제점은 객체 하나를 만드려면 여러 setter 메서드를 호출해줘야하고 그와중에 일관성이 사라진다. 들어가는 값이 유효한지 확인하는 방법이 사라지고 여러 setter 매서드들을 호출하면서 물리적으로 코드가 떨어져있기 때문에 디버깅도 만만치 않다.

세번째 대안으로 빌더 패턴이있다. 빌더패턴을 사용하면 완성된 객체를 일관성있게 불변으로 객체를 생성할 수 있다.

### 아이템3 private 생성자나 열거 타입으로 싱글턴임을 보증하라



싱글턴: 인스턴스를 오직하나만 생성할 수 있는 클래스

static 은 처음에 어플리케이션이 실행되었을때 가장 먼저 메모리에 올라가기 때문에 아래 코드처럼의 싱글톤이 가능

```java
public class Elvis {
    public static final Elvis INSTANCE = new Elvis();

    private Elvis() {

    }


}
```

유일하게 인스턴스를 두개 만들 수 있는 방법은 리플렉션(아이템65)을 활용해서 호출하는것이다. 이런 공격을 방어하려면 두번째 생성자 호출시 예외날리면 됨

두번째 방법은 정적 팩터리 방식의 싱글턴

```java
public class Elvis {
    private static final Elvis INSTANCE = new Elvis();

    private Elvis() {

    }

    public static Elvis getInstance() {
        return INSTANCE;
    }
}
```

이 방법이 public 방식과 다른 점은

1. API를 바꾸지 않고도 싱글턴이 아니게 변경할 수 있다. 예를 들어 호출하는 스레드별로 다른 인스턴스를 넘겨줄 수 있게 할 수 있다 (이게 무슨말?)
2. 제네릭 싱글턴 팩터리 UnaryOperator
3. `Supplier<Elvis>` 형식

마지막 방법은 원소가 하나인 enum 사용

```java
public enum Kyu {
    INSTANCE
}
```



### 아이템6 불필요한 객체 생성을 피하라

* 생성자 대신 정적팩터리메서드를 사용하면 피할수있다
* 비싼 객체는 캐싱하여 재사용하라
  * 코드6-1, 코드6-2
    * 유한 상태 머신
* 어댑터 or 뷰
* 오토박싱을 피해라
* 그렇다고 무조건적으로 객체 생성을 피해라는 것은 아니다
  * 명확성, 간결성, 기능을 위해 추가로 생성하능것은 일반적으로 좋은일이다
* 자신만의 객체 풀을 만들지마라
  * 디비커넥션은 생성비용이 워낙비싸니 그렇게하는게 좋지만 일반적으론 코드를 헷갈리게하고 메모리사용량을 늘리고 성능을 떨어뜨린다
* 방어적 복사가 필요한 상황도 있으므로 무조건적으로 객체 생성을 피하는것은 바람직하지않다



## 3장..



### 아이템11

```java
package org.example;

import java.util.HashMap;
import java.util.Map;

public class Main {
    public static void main(String[] args) {
        Map<PhoneNumber, String> map = new HashMap<>();
        map.put(new PhoneNumber(10, 1234, 3456), "hey");

        System.out.println(map);

        // null이 나오는 이유는? -> 앞에서 put한거랑 지금 get하거랑 서로 다른 객체이기 때문
        // 더 나아가서 HashMap은 해시코드가 서로 다른 엔트리끼리는 동치성 비교를 시도조차 안하도록 최적화 되어있다
        // 그런데 둘다 논리적으로 같은 객체이다
        // null이 아니라 의도하는 "hey" 가 나오게 하려면? -> hashCode 를 override해줘야한다
        System.out.println(map.get(new PhoneNumber(10, 1234, 3456)));


        System.out.println();
        System.out.println();
        System.out.println();
        System.out.println();
        System.out.println();
        System.out.println();
/////////////////////////////////////////////////
/////////////////////////////////////////////////
/////////////////////////////////////////////////
        // 아래 a,b는 hashCode가 같음
        String a = "Z@S.ME";
        String b = "Z@RN.E";

        System.out.println(a.hashCode());
        System.out.println(b.hashCode());

        HashMap<String, Integer> hasnMap2 = new HashMap<>();
        hasnMap2.put(a, 30);
        hasnMap2.put(b, 40);

        System.out.println(a.equals(b)); // false
        System.out.println(a.hashCode()); // -1656719047
        System.out.println(b.hashCode()); // -1656719047
        System.out.println(hasnMap2.size()); // 2
        System.out.println(hasnMap2.get(a)); // 30
        System.out.println(hasnMap2.get(b)); // 40

        // 위 코드가 의미하는건
        // 두개의 HashCode가 같게 나와도 HashMap이 잘 처리해서 다른 키로 구분해주고있음

        System.out.println();
        System.out.println();
        System.out.println();
        System.out.println();
        System.out.println();
        System.out.println();
        /////////////////////////////////////////////////
/////////////////////////////////////////////////
/////////////////////////////////////////////////

        Person person1 = new Person("kim");
        Person person2 = new Person("kim");

        HashMap<Person, Integer> hashMap = new HashMap<>();
        hashMap.put(person1, 10);
        hashMap.put(person2, 20);

        System.out.println(person1.equals(person2));
        System.out.println(person1.hashCode());
        System.out.println(person2.hashCode());
        System.out.println(hashMap.size());
        System.out.println(hashMap.get(person1));
        System.out.println(hashMap.get(person2));

        /////////////////////////////////////////////////
/////////////////////////////////////////////////
/////////////////////////////////////////////////
        System.out.println();
        System.out.println();
        System.out.println();
        System.out.println();
        System.out.println();
        System.out.println();

        PhoneNumber number1 = new PhoneNumber(10, 1234, 3456);
        PhoneNumber number2 = new PhoneNumber(10, 1234, 3456);

        HashMap<PhoneNumber, Integer> hashMap2 = new HashMap<>();
        hashMap2.put(number1, 10);
        hashMap2.put(number2, 20);

        System.out.println(number1.equals(number2));
        System.out.println(number1.hashCode());
        System.out.println(number2.hashCode());
        System.out.println(hashMap2.size());
        System.out.println(hashMap2.get(new PhoneNumber(10, 1234, 3456)));
        // 위에 두개는 hashCoder가
//        1285044316
//        1607460018
        // HashMap 같은경우에 put,get 할때 hash값을 이용하므로 위에 두객체가 equals가 true가 나왔다고 해도
        // get을 하면 null이 나오는 것이다, 이를 방지하기위해 논리적으로 두 객체가 같도록 equals를 재정의했으면 hashCode도 재정의해줘야한다
    }
}


class Person {
    String name;

    Person(String name) {
        this.name = name;
    }

    @Override
    public boolean equals(Object obj) {
        Person anotherObj = (Person) obj;
        return this.name.equals(anotherObj.name);
    }
}

class PhoneNumber {
    private int first;
    private int second;
    private int third;

    public PhoneNumber(int first, int second, int third) {
        this.first = first;
        this.second = second;
        this.third = third;
    }

    @Override
    public boolean equals(Object o) {
        PhoneNumber anotherObj = (PhoneNumber) o;
        return this.first == anotherObj.first &&
                this.second == anotherObj.second &&
                this.third == anotherObj.third;
//        if (this == o) return true;
//        if (o == null || getClass() != o.getClass()) return false;
//        PhoneNumber that = (PhoneNumber) o;
//        return first == that.first && second == that.second && third == that.third;
    }

//    @Override
//    public int hashCode() {
//        return Objects.hash(first, second, third);
//    }
}
```
