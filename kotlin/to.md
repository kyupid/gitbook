# \[인프런] 자바 to 코틀린 입문



### Lec01 코틀린에서 변수를 다루는 방법

* 모든 변수는 var / val을 붙여주어야한다
  * var: 변경가능 / val: 변경불가능
* 타입을 명시하지 않아도 타입이 추론된다
* Primtive Type과 Reference Type을 구분하지 않아도 된다
* Null이 들어갈수있는 변수는 타입 뒤에 `?`를 붙인다
  * `?`일시에 다른 타입으로 간주된다
* 객체 인스턴스화시에 `new` 사용하지 않는다

### Lec02. 코틀린에서 null을 다루는 방법

* 코틀린에서 null이 들어갈 수 있는 타입은 완전히 다르게 간주된다
  * 한 번 null 검사를 하면 non-null임을 컴파일러가 알 수 있다.
* null이 아닌 경우에만 호출되는 Safe Call (`?.`)이 있다.
* null인 경우에만 호출되는 Elvis 연산자 (`?:`)가 있다.
* 코틀린에서 자바코드를 사욯알때 플랫폼 타입 사용에 유의해야한다.
  * Java 코드를 읽으며 널 가능성 확인 / 코틀린으로 한번 래핑 (자바코드의 진입을 최소화)





### Lec03. 코틀린에서 Type을 다루는 방법

* 코틀린의 변수는 초기값을 보고 타입을 추론하며, 기본 타입들 간의 변환은 명시적으로 이루어진다

```kotlin
val foo = 10L // 초기값으로 타입추론 -> Long


val foo = 10L
var bar = 1
bar = foo.toInt() // 기본 타입들 간의 명시적 변환
```

* 코틀린에서는 is, !is, as, as? 를 이용해서 타입을 확인하고 캐스팅한다

```kotlin
if (hello is World) {
	// ...
	// hello의 타입이 World 라면 스마트 캐스트라고 해서 World의 함수를 사용할수있음
	hello.printWorld()
}
```

* Any: Java의 Object 역할, Primitive Type의 최상위타입
* Unit: Java의 void와 동일한 역할
* Nothing: 함수가 정상적으로 끝나지 않았다는 사실을 표현하는 역할
  * 무조건 예외를 반환하는 함수 / 무한 루프 함수 등
* Sring interpolation: 코틀린에서 `${변수}` 처럼 사용가능
* `"""` 큰 따옴표 3개로

### Lec04. 코틀린에서 연산자를 다루는 방법

* 단한연산자, 산술연산자, 산술대입연사자 자바와 같다
* 비교 연산자 사용법도 자바와 똑같다
  * 객체간에도 자동 호출되는 compareTo를 이용해 비교 연산자를 사용할 수 있다
* in, !in, / a..b / a\[i] / a\[i] = b 와 같이 코틀린에서 새로 생긴 연산자도 있다
* 객체끼리 연산자를 직접 정의할 수 있다

```kotlin
data class Money(
   val amount: Long
) {
    operator fun plus(other: Money): Money {
        return Money(this.amount + other.amount)
    }
}
```
