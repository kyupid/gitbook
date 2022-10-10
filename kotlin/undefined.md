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



### Lec05. 코틀린에서 조건문을 다루는 방법

* if / if-else 모두 자바와 문법이 동일하다
* 단 코틀린에서는 Expression으로 취급된다
  * 때문에 if 앞에 return을 넣을 수 있다
  * 삼향연산자가 없다

```kotlin
fun getPassOrFail(score: Int): String {
	return if (score > 50) {
		"P"
	} else {
		"F"
	}
}
```

* 자바의 switch는 when으로 대체되었고 더 강력한 기능을 가진다

```kotlin
fun startsWithA(obj: Any): Boolean {
    return when (obj) {
        is String -> obj.startsWith("A")
        else -> false
    }
}

fun judgeNumber(number: Int) {
    when (number) {
        1, 0, -1 -> println("yes")
        else -> println("no")
    }
}

fun judgeNumber2(number: Int) {
    when {
        number == 0 -> println("sda")
        number % 2 == 0 -> println("asdas")
        else -> println("ASdasd")
    }
}
```

### Lec06. 코틀린에서 반복문을 다루는 방법

* foreach는 `:` 대신 `in` 을 사용한다

```kotlin
    val numbers = listOf(1L, 2L, 3L)
    for (number in numbers) {
        println(number)
    }
```

* for문은 다르다

```kotlin
    for (i in 1..3) { // 시작값1 끝값3 공차가 0인 등차수열 생성 IntProgression
        println(i)
    }

    for (i in 3 downTo 1) { // 시작값1 끝값3 공차가 -1인 등차수열 생성 IntProgression
        println(i)
    }

    for (i in 1..5 step 2) { // 시작값1 끝값3 공차가 2인 등차수열 생성 IntProgression
        println(i)
    }
```

* downTo, step 도 함수이다. (중위함수)
  * `변수.함수이름(arg)` 대신 `변수 함수이름 arg`
* while, do while 은 똑같다

### Lec07. 코틀린에서 예외를 다루는 방법

* try catch finally 구문은 문법적으로 완전 동일
  * 코틀린에서는 try catch가 expression이다
* 코틀린에서는 모든 예외는 Unchecked Exception이다
* 코틀린에서는 try with resources 구문이 없다. 대신 코틀린의 언어적 특징을 활용해 close 를 해준다

```kotlin
class FilePrinter {

    fun readFile(path: String) {
        BufferedReader(FileReader(path)).use { reader ->
            println(reader.readLine())
        }
    }

    fun readFile() {
        val currentFile = File(".")
        val file = File(currentFile.absolutePath + "/a.txt")
        val reader = BufferedReader(FileReader(file))
        println(reader.readLine())
        reader.close()
    }
}
```

### Lec08. 코틀린에서 함수를 다루는 방법

* body가 하나의 값으로 간주되는 경우 block을 없앨 수도 있고, block이 없다면 반환 타입을 없앨 수도 있다

```kotlin
fun max(a: Int, b: Int) = if (a > b) a else b
```

* 함수 파라미터에 기본값을 설정해줄수있다
* 함수를 호출할때 특정파라미터를 지정해 넣을수도 있다
* 가변인자에는 vararg 키워드를 사용하고 가변인자 함수를 배열을 넣어 호출하고 싶을땐 `*`를 붙인다



### Lec09. 클래스를 다루는 방법

* 코틀린에서는 필드를 만들면 getter와 필요에따라 setter가 자동으로 생긴다
  * 때문에 이를 프로퍼티라고 부른다
* 생성자는 아래처럼 주생성자와 부생성자로 나뉜다

```kotlin
fun main() {
    Person()
}

class Person(
    val name: String,
    var age: Int
) {
    init {
        if (age <= 0) {
            throw IllegalAccessException("나이는 ${age}일 수 없습니다")
        }
        println("초기화 블록")
    }

    constructor(name: String) : this(name, 1) {
        println("첫번쨰부생성자")
    }

    constructor() : this("hey") {
        println("두번쨰")
    }

}
```

```
> Task :PersonKt.main()
초기화 블록
첫번쨰부생성자
두번쨰
```

* 하지만 코틀린은 이것보다 default parameter를 권장한다

```kotlin
class Person(
    val name: String = "hey",
    var age: Int = 3
) {
	// ...
}
```

* getter,setter는 이미 선언되어져있다. 기능을 추가할때 custom getter를 추가할수있다

```kotlin
    fun isAdult(): Boolean {
        return this.age >= 20
    }

    val isAdult: Boolean
        get() = this.age >= 20


    val isAdult: Boolean
        get() {
            this.age >= 20
        }
```

* custom getter, custom setter에서 무한루프륵 막기 위해 field라는 키워드를 사용한다
  * 이를 backing field라고 부른다
