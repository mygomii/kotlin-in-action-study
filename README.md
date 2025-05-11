# 📌 kotlin-in-action-study

<details>
<summary><strong>2.1 기본 요소: 함수와 변수</strong></summary>

## 2.1.1 첫 번째 코틀린 프로그램 작성 
  ```kotlin
fun main() {
  println("Hello World!")
}
```

- 함수를 선언할 때 `fun`  키워드 사용
- 코틀린은  간결성을 강조
- 세미클론(;)을 붙이지 않는다.

## 2.1.2 파라미터와 반환값이 있는 함수 선언

```kotlin
fun max(a: Int, b: Int): Int {
  return if (a > b) a else b 
}
```

- `max` 는 함수이름
- `(a: Int, b: Int)` 는 파라미터
- `Int` 는 반환타입
- `return if (a > b) a else b` 함수 본문

<aside>
💡

문(statement)과 식의 구분 

코틀린에서는 if는 식이지 문이 아님, 식은 값을만들어내며 다른 식의 하위 요소로 계산에 참여할 수 있는 반면, 문은 자신을 둘거싸고 있는 가장 안쪽 블록의 최상위 요소로 존재하면 아무런 값을 만들어내지 않는다는 차이가 있음. 

</aside>

## 2.1.3 식 본문을 사용해 함수를 더 간결한게 정의

```kotlin
fun max(a: Int, b: Int): Int = if (a > b) a else b 
```

- 위의 형태는 *식 분문 함수(expression body function)*이라고 부른다

모든 함수는 반환 타입이 정해져야 함, 하지만 위 본문 함수의 경우 굳이 반환타입을 적지 않아도 컴파일러가 함수 본문 식을 분석해서 식의 결과 타입을 함수 반환 타입으로 정해줌 ⇒ 이런 부석을 ‘***타입 추론’*** 이라 부름

---

## 2.1.4 데이터를 저장하기 위해 변수 선언

코틀린에서 변수 선언은 키워드(val 또는 var)로 시작하고 그 뒤에 변수이름이 옴, 그리고 변수 이름 뒤에 타입을 명시할 수 있음 

```kotlin
val question: String = "이건 질문이다" 
```

## 2.1.5 변수를 읽기 전용 변수나 제대입 가능 변수로 표시

`val` 는 value에서 따옴, 읽기 전용 참조(read-only reference)를 선언. val로 선언된 변수는 단 한 번만 대입할수 있음 (자바에서는 final) 

`var` 는 variable에서 따옴, 제대입 가능한 참조(reassignable reference) 선언, 초기화가 이뤄진 다음이라도 다른 값을 대입할 수 있음 

## 2.1.6 더 쉽게 문자열 형식 지정 : 문자열 템플릿

```kotlin
fun main() {
  val name = "고미정"
  println("Hello $name") // <= 이렇게 간단하게 사용 가능 
}
```
</details>

<details>
<summary><strong>2.2 행동과 데이터 캡슐화 : 클래스와 프로퍼티</strong></summary>

- 객체지향 언어로 클래스라는 추상화를 제공, 더 적은 양의 코드로 대부분의 공통적인 작업을 수행할수 있음

(Java)

```java
public class Person {
  private final String name;
  public Person(String name) {
    this.name = name;
  }
  public String getName() {
    return name;
  }
}
```

(Kotlin)

```kotlin
class Person(val name: String)
```

- 위 자바코드에 비해 kotlin는 이렇게 간단하게 작성할수 있다

## 2.2.1 클래스와 데이터를 연관시키고, 접근 가능하게 만들기 : 프로퍼티

- 클래스라는 개념은 데이터를 캡슐화하고, 캡슐화한 데이터를 다루는 코드를 한 주체 안에 가두는 것
- 자바에서는 데이터를 필드에 저장하면 멤버 필드의 가시성은 보통 비공개(private), 접근자 메서드를 제공   ⇒ 자바에서는 필드와 접근자를 한데 묶어 ‘프로퍼티(property)’ 라고 부름
- 코틀린은 프로퍼티를 언어 기본 기능으로 제공

```kotlin
class Person (
  val name: String, // 읽기 전용 프로퍼티로 getter 를 만들어냄
  var isStudent: Boolean // 쓸 수 있는 프로퍼티로 setter, getter를 만들어냄
)
```

## 2.2.2 프로퍼티 값을 저장하지 않고 계산 : 커스텀 접근자

```kotlin
class Rectangle(val height: Int, val width: Int) {
  val isSquare: Boolean 
    get() {
      return height == width 
    }
				
  // get() = height == width  <= 이렇게 사용해도 된다 
}
```

- 위 코드 처럼 사용할 수 있다.
- 커스텀 게터를 정의하는 방식과 클래스 안에 함수를 정의하는 방식 중 성능 차이는 없지만, 가독성 차이는 있다.  (요구사항에 따라 다르게 구현하면 될듯)

## 2.2.3 코틀린 소스코드 구조 : 디렉터리와 패키지

- 코틀린은 클래스를 조직화하기 위해 패키지라는 개념을 사용(자바 패키지와 비슷)
</details>

<details>
<summary><strong>2.3 선택 표현과 처리 : enum과 when</strong></summary>

- `when`은 자바의 `switch`를 대신하지만 훨씬 더 강력하며 더 자주 사용 되는 프로그래밍 요소
- 코틀린에서는 `enum class` 를 사용하지만 자바에서는 `enum` 을 사용

## 2.3.1 enum class와 enum 상수 정의

- enum은 자바 선언보다 코틀린 선언에 더 많은 키워드를 써야하는 흔치 않은 예

```kotlin
enum class Color {
  RED, ORANGE, YELLO;
}
```

- 이 예제에서는 코틀린에서 유일하게 세미콜론(;)이 필수인 부분을 볼 수 있음

## 2.3.2 when으로 이넘 클래스 다루기

```kotlin
fun getMnemonic(color: Color) {
  when (color) {
    Color.RED -> "RED"
    Color.GREEN -> "Green"
    Color.BLUE -> "Blue"
  }
}

fun main() {
  getMnemonic(Color.BLUE) 
  // Blue 
}

```

- 자바와 달리 break를 넣지 않아도 됨

## 2.3.3 when식의 대상을 변수에 캡처

```kotlin
enum class Color(val r: Int, val g: Int, val b: Int) {
  RED(255, 0, 0),
  GREEN(0, 255, 0),
  BLUE(0, 0, 255),
}

fun measureColor() = Color.RED

fun getWarm() = when (val color = measureColor()) {
  Color.RED -> "red: ${color.r}"// when안에서 만든 변수의 프로퍼티에 접근할 수 있음 
  Color.GREEN -> "greed : ${color.g}"
  Color.BLUE -> "blue : ${color.b}"
}
```

## 2.3.5 인자 없는 when 절 사용

```kotlin
val score = 75

when { // <- 인자가 없음 
  score >= 90 -> println("A")
  score >= 80 -> println("B")
  score >= 70 -> println("C")
  score >= 60 -> println("D")
  else -> println("F")
}
```

## 2.3.6 스마트 캐스트: 타입 검사와 타입 캐스트 조합

```kotlin
interface Expr

class Num(val value: Int) : Expr
class Sum(val left: Expr, val right: Expr) : Expr

fun eval(e: Expr): Int = when(e) {
  is Num -> e.value
  is Sum -> eval(e.left) + eval(e.right)
  else -> throw IllegalArgumentException("Unknown expression")
}
```

```kotlin
fun eval(e: Expr): Int {
  if (e is Num) {
    val n = e as Num // 여기서 Num으로 타입을 변환하는데, 이는 불필요한 중복
      return n.value
  }

  if (e is Sum) {
    return eval(e.right) + eval(e.left) // < 변수 e에 대해 스마트 캐스트를 사용
  }
  throw IllegalArgumentException("Unknown expression")
}

fun main() {
  println(eval(Sum(Sum(Num(1), Num(2)), Num(4))))
}

```

- `is`  는 자바의 `instanceof`  와 같다
- 코틀린의 is는 약간의 편의를 추가로 제공
</details>

<details>
<summary><strong>2.4 대상 이터레이션: while과 for 루프 </strong></summary>


- 코틀린의 이터레이션은 자바 등 다른 언어에서 사영호난 방법과 아주 비슷
- `while`은 다른 언어와 마찬가지인 전통적인 형식을 따름

## 2.4.1 조건이 참인 동안 코드 반복 : while 루프

- while 문

```kotlin
while(조건) {
  if(shouldExit) {
    break
  }
}
```

- do-while문

```kotlin
do {
  if (shouldExit) {
    continue
  }
} while (조건)
```

- 내포된 루프의 경우 코틀린에서는 레이블을 지정할 수 있음. 그 후 `break` 나 `continue` 를 사용할 때 레이블을 참조할수 있음

```kotlin
outer@while(outerCondition) {
  while(innerCondition) {
    //if(shouldExit) break 
    //if(shouldExit) continue

    // 레이블을 지정하면 지정한 루프를 빠져나갈수 있음
    //if(shouldExit) break@outer
    //if(shouldExit) continue@outer	
  }
}
```

## 2.4.2 수에 대해 이터레이션: 범위와 순열

- 코틀린의 범위는 폐구간, 즉 양끝을 포한하는 구간

```kotlin
val oneToTen = 1..10 // (1부터 10까지)
```

- 이런 식으로 어ㅈ떤 범위에 속한 값을 일정한 순서로 이터레이션하는 경우를 **순열(progresstion)이라고 부름**
- `downTo` 는 역방향 순열

## 2.4.3 맵에 대해 이터레이션

방법1. 

```kotlin
val collection = listOf("red", "blue", "green")
for (color in collection) {
  print("$color")
}
```

방법2

```kotlin
val collection = listOf("red", "blue", "green")
for ((index, element) in collection.whitIndex()) { // <- 인덱스와 함께 컬렉션을 이터레이션 함 
   print("$index, $element")
}
```

## 2.4.4 in으로 컬렉션이나 범위의 원소검사

- in 연산자를 사용해 어떤 값이 범위에 속하는지 검사할 수 있음

```kotlin
  when (ch) {
     in '0'..'9' -> println("$ch 는 숫자입니다.")
     in 'a'..'z', in 'A'..'Z' -> println("$ch 는 알파벳입니다.")
     else -> println("$ch 는 특수문자입니다.")
  }
```
</details>

<details>
<summary><strong>2.5 코틀린에서 예외 던지고 잡아내기</strong></summary>



- 코틀린에서 예외 처리는 자바나 다른 언어의 예외 처리와 비슷
- `throw` 키워드를 사용해 예외를 던질 수 있음
    
    ```kotlin
    if(percentage !in 0..100) {
	throw IllegalArgumentException("a percentage value nust be between - and 100") 
    }
    ```
    

## 2.5.1 try, catch, finally를 사용한 예외 처리와 오류 복구

```kotlin
try {
    // 예외가 발생할 수 있는 코드
} catch(e: Exception) {
    // 예외 처리 코드
} finally {
    // 항상 실행되는 코드 (예외 여부 상관없음)
}
```

```kotlin
fun parseNumber(input: String): Int {
    return try {
        input.toInt()
    } catch (e: NumberFormatException) {
        println("오류 발생: 숫자가 아닌 입력값 [$input]")
        -1 // 예외 발생 시 기본값으로 -1 반환하여 복구
    } finally {
        println("입력값 처리 완료: $input")
    }
}
```

- 자바에서는 체크 예외가 메서드 시그니처의 일부

| **예외 종류**	 | 	**메서드 시그니처에 명시 필요 여부** |
| --- | --- |
| Checked Exception (IOException, SQLException)	 | 필수 (꼭 명시해야 함) |
| Unchecked Exception (NullPointerException, ArithmeticException) |  불필요 (명시하지 않아도 됨 |

## 2.5.2 try를 식으로 사용

- 지금까지는 try를 문으로만 사용했지만, try의 결과를 변수에 대입 할 수 있음
- 아래 코드처럼 catch에서 반환할 수 도 있음
    
    ```kotlin
    fun parseInt(input: String): Int {
        return try {
            input.toInt()
        } catch (e: NumberFormatException) {
            -1  
        }
    }
    ```
</details>
<hr>
<details>
<summary><strong>3.1 코틀린에서 컬렉션 만들기 </strong></summary>



``` kotlin
val set1 = setOf(1,7, 53)

val list = listOf(1, 7, 53)
val map = listOf(1 to "one", 7 to "seven", 53 to "fifity-three")
```

- 여기서 `to` 는 언어가 제공하는 특별한 키워드가 아니라 일반 함수라는 점에 유의

```kotlin
println(set.javaClass) // class java.util.LinkedHasSet

println(list.javaClass) // class java.util.Arrays$ArrayList

println(map.javaClass) // class java.util.LinkedHashMap
```

- 결과에서 알 수 있는 것처럼 코틀린은 표준 자바 컬렉션 클래스를 사용
- 자바와 달리 코틀린 컬렉션 인터페이스가 디폴트로 읽기 전용이라는 사실을 알고있자	
</details>

<details>
<summary><strong>3.2 함수를 호출하기 쉽게 만들기</strong></summary>



- 컬렉션을 만드는 방법을 살펴봤으므로 뭔가 간단한 일을 하자?

```kotlin
val list = listOf(1, 2, 3)
println(list) 
// [1, ,2, 3]
```

## 3.2.1 이름 붙인 인자

- 첫 번째 문제는 함수 호출 부분의 가독성

```kotlin
val items = listOf("apple", "banana", "cherry")
val result = items.joinToString(separator = ", ", prefix = "[", postfix = "]")
println(result) 
```

- 코틀린으로 작성한 함수를 호출할 때는 함수에 전달하는 인자 중 일부의 이름을 명시 할 수 있음
- 전달하는 모든 인자의 이름을 지정하는 경우 심지어 인자의 수선를 변경할 수 있음

## 3.2.2 디폴트 파라미터 값

```kotlin
fun <T> .joinToString(
    collection: Collection<T>,
    separator: String = ", ",
    prefix: String = "",
    postfix: String = "".
): String 
```

- collection을 제외하고 기본값이 지정된 파라미터 값임
- 함수를 호출할때 모든 인자를 쓸 수도 있고, 일부를 생략할 수도 있음
- 함수의 디폴트 파라미터 값은 함수를 호출하는 쪽이 아니라 함수 선언 쪽에 인코딩 된다는 사실!, 어떤 클래스 안에 정의된 함수의 기본값을 바꾸고 그 클래스가 포함된 파일을 재컴파일하면 그 함수를 호출하는 코드 중 값을 지정하지 않은 모든 이자는 자동으로 바뀐

기본값을 적용받음

## 3.2.3 정적인 유틸리티 클래스 없애기: 최상위 함수와 프로퍼티

- 자바에서는 모든 코드를 클래스의 메서드로 작성해야만 한다는 사실을 알고 있음
- **최상위 함수와 프로퍼티**
    - Kotlin에서는 클래스 내부가 아닌 파일의 최상위에 직접 함수를 선언할 수 있음. 이렇게 선언된 함수는 해당 패키지 내에서 자유롭게 사용할 수 있음
- **적 메서드 불필요**
    - Java에서는 정적 메서드를 담기 위해 유틸리티 클래스를 만들어야 하지만, Kotlin에서는 이런 패턴이 필요 없음
- **JVM 상호 운용성**
    - 최상위 함수와 프로퍼티는 컴파일 시 파일 이름에 따른 클래스로 변환됨. 필요하다면 @file:JvmName("CustomName") 어노테이션을 사용해 클래스 이름을 변경할 수 있음
- 최상위 함수 예시
    
    ```kotlin
    fun isNullOrEmpty(s: String?): Boolean = s == null || s.isEmpty()
    ```
    
- 최상위 프로퍼티 예시
    
    ```kotlin
    val defaultGreeting: String = "Hello, world!"
    ```
</details>

<details>
<summary><strong>3.3 메서드를 다른 클래스에 추가: 확장 함수와 확장 프로퍼티 </strong></summary>



- 확장 함수는 단순
- 확장 함수는 어떤 클래스의 멤버 메서드인 것처럼 호출할 수있지만, 그 클래스의 밖에 선언된 함수

```kotlin
fun String.lastChar(): Char = this.get(this.length - 1)
```

- 함수 이름 앞에 그 함수가 확장할 클래스의 이름을 덧붙이는 것 → 이런 클래스를 수신 객체 타입(receiver type)라 부름
- 확장 함수 호출 . 시여러분이 호출하는 대상 값(객채)를 수신 객체(receiver object)라고 부름

```kotlin
println("Kotlin".lastChar()) 
// n 
```

- 확장 함수 내부에서는 일반적인 인스턴스 메서드의 내부와 마찬가지로 수신 객체의 메서드나 프로퍼티를 바로 사용할 수 있음
- 하지만 확장 함수가 캡슐화를 깨지 않는 다는 사실
- 클래스 안에서 정의한 메서드와 달리 확장 함수안에서는 클래스 내부에서만 사용 할수 있는 `private` , `protected` 를 사용 할 수 없음

## 3.3.1 임포트와 확장 함수

- 확장 함수를 쓰려면 다른 클래스나 함수와 마찬가지로 해당 함수를 임포드를 해야함

## 3.3.2 자바에서 확장 함수 호출

```kotlin
char c = StringUtilKt.lastChat("Java");
```

## 3.3.3 확장 함수로 유틸리티 함수 정의 (생략)

## 3.3.4 확장 함수는 오버라이드를 할수 없다

- 확장 함수는 오버라이드를 할 수 없음

## 3.3.5 확장 프로퍼티

- 확장 함수와 마찬가지로 확장 프로퍼티를 사용하면 함수가 아니라 프로퍼티 형식의 구문으로 사용할수 있는 api를 추가할 수 있음
- 프로퍼티라는 이름으로 불리기는 하지만 상태를 저장할 적절한 방법이 없기때문에 실제로 확장 프로퍼티는 아무 상태도 가질 수 없음

```kotlin
val String.lastChar: Char
	get() = get(length - 1)
```

- 확장 프로퍼티도 단지 프로퍼티에 수신 객체 클래스가 추가됐을 뿐임을 알 수 있음
- 뒷받침하는 필드가 없어 기본 게터 구현을 제공 할 수 없으므로 최소한 게터는 꼭 정의를 해야함
- 초기화 코드에서 계산한 값을 담을 장소가 전혀 없으므로 초기화 코드를 쓸 수 없음	
</details>

<details>
<summary><strong>3.4 컬렉션 처리: 가변 길이 인자, 중위 함수 호출, 라이브러리 지원 </strong></summary>


 - `vararg` 키워드를 사용하면 호출 시 인자 개수가 달라질 수 있는 함수를 정의 할 수 있음
- `infinx(중위)` 함수 호출 구문을 사용하면 인자가 하나뿐인 메서드를 간편하게 호출 할 수 있음
- `구조 분해 선언` 을 사용하면 복합적인 값을 분해해여 여러변수에 나눠 담을 수 있음

## 3.4.1 자바 컬렉션 API 확장

```kotlin
fun <T> List<T>.last(): T { /* 마지막 원소를 반환함 */}
fun Collection<Int>.max(): Int { /* 컬렉션의 최댓값을 찾음 */}
```

- 위 예시 처럼 확장함수로 사용 가능

## 3.4.2 가변 인자 함수 : 인자의 개수가 달라질 수 있는 함수 정의

- 리스트를 생성하는 함수를 호출할 대 원하는 만큼 많이 원소를 전달 할 수 있음

```kotlin
val list = listOf(2,3,4,5,6)
```

```kotlin
fun listOf<T>(vararg values: T): List<T> {}
```

- 이 함수는 호출할 때 원하는 개수만큼 여러값을 인자로 넘기면 배열에 그 값들을 넣어주는 언어 기능인 가변 길이 인자(vararg) 사용

- 이미 배열에 들어있는 원소를 가변 길이 인자로 넘길 떼도 코틀린과 자바 구문이 다름
- 자바에서는 배열을 그냥 넘기면 되지만 코틀린에서는 배열을 명시적으로 풀어 배열의 각 원소가 인자로 전달되게 해야함 → 이런 기능을 스프레드(spread) 연산자라 함
- 스프레드 연산은 배열앞에 *를 붙이기만 하면 됨

```kotlin
fun main(args: Array<String>) {
	val list = listOf("args:", *args)
}
```

## 3.4.2 쌍(튜플) 다루기 : 중위 호출과 구조 분해 선언

```kotlin
val map = mapOf(1 to "One", 7 to "seven", 3 to "three")
```

- `to` 라는 단어는 kotlin키워드가 아님 이 코드는 중위 호출이라는 특별한 방식으로 `to` 라는 일반 메서드를 호출
    
    ```kotlin
    infix fun Any.to(other: Any) = Pair(this, other)
    ```
    
    - 이 `to` 함수는 `Pair` 의 인스턴스를 반환
    - `Pair` 의 내용을 갖고 두 변수를 즉시 초기화 할 수 있음
        
        ```kotlin
        val (number, name) = 1 to "One"
        ```
        
        - 이런 기능을 구조 분해 선언 이라고 부름
</details>

<details>
<summary><strong>3.5 문자열과 정규식 다루기 </strong></summary>


- 코틀린 문자열은 자바 문자열과 똑같음
- 코틀린 코드가 만들어낸 문자열을 아무 자바 메서드에 넘겨도 되며, 자바 코드에서 받은 문자열을 아무 코틀린 표준 라이브러리 함수에 전달해도 전혀 문제 없음

## 3.5.1 문자열 나누기

- `String` 의 `split` 메서드를 알고 있을것이다
- `“12.345-6.A”.split(.)` 라는 호출의 결과가 `[12, 345-6, A]` 배열이라고 생각하는 실수를 저지를는 개발자가 많음 ⇒ 하지만 `split` 은 빈 배열을 반환함
- 이유는 `split` 이 정규식(regular expression)을 구분 문자열로 받아 . 그정슈식에 따라 문자열을 나누기 때문 → 이 경우 마침표는 모든 문자를 나타내는 정규식으로 해석
- 정규식을 파라미터로 받는 함수는 `String`이 아닌 `Regex` 타입의 값을 받음

```kotlin
fun main() {
	println("12.345-6.A".split("\\.|-".toRegex())) // <- 정규식을 명시적으로 받음
	// [12, 345, 6, A]
}
```

- 하지만 이렇게 간단한 경우 정규식을 사용할 필요 x
- `split` 확장 함수 오버로딩한 버전 중에는 구분 문자열을 하나 이상 인자로 받는 함수가 있음

```kotlin
fun main() {
	println("12.345-6.A".split('.', '-')) // 이렇게 사용해도 똑같은 결과를 얻을 수 있음 
}
```

## 3.5.2 정규식과 3중 따옴표로 묶은 문자열

- 코틀린에서는 정규식을 사용하지 않고도 문자열을 쉽게 파싱할 수 있음

## 3.5.3 여러 줄 3중 따옴표 문자열

- 3중 따옴표 문자열은 문자열 이스케이프를 피하기 위해서만 사용하지는 않음

```kotlin
fun main() {
    val multilineString = """
        첫 번째 줄입니다.
        두 번째 줄입니다.
        세 번째 줄입니다.
    """.trimIndent()

    println(multilineString)
}

//첫 번째 줄입니다.
//두 번째 줄입니다.
//세 번째 줄입니다.
```

- 3중 따옴표 문자열 안에 문자열 템플릿을 사용할 수 있음 그러나 3중 따옴표 문자열 안에서는 이스케이프를 할 수 없기 때문에 문자열 내용에서 $나 유니코드 이스케이프를 사용하고 싶을 때는 내포 식을 사용해야함
</details>

<details>
<summary><strong>3.6 코드 깔끔하게 다듬기: 로컬 함수와 확장</strong></summary>

 - 많은 개발자가 좋은 코드의 중요한 특징 중 하나가 중복이 없는 것이라 믿음 →ㅇㅈㅇㅈ
    
    → 이런 원칙에 대해 **반복하지 말라(DRY: Don’t Repeat Yourself)** 라는 이름도 있음 
    
- 자바에서는 쉽지않지만 코틀린에는 더 깔끔한 해법이 있음
- 코틀린에서는 함수에서 추출한 함수를 원래의 함수 내부에 내포 시킬 수 있음

- 코드 중복을 보여주는 예제

```kotlin
class Student(val name: String, val korean: Int, val english: Int, val math: Int) {
    fun koreanAverage(): Double {
        return korean / 100.0 * 100
    }

    fun englishAverage(): Double {
        return english / 100.0 * 100
    }

    fun mathAverage(): Double {
        return math / 100.0 * 100
    }
}
```

- 로컬 함수를 사용해 코드 중복 줄이기

```kotlin
class Student(val name: String, val korean: Int, val english: Int, val math: Int) {
    
    // 공통 로직을 메서드로 추출
    private fun calculateAverage(score: Int): Double {
        return score / 100.0 * 100
    }

    fun koreanAverage(): Double {
        return calculateAverage(korean)
    }

    fun englishAverage(): Double {
        return calculateAverage(english)
    }

    fun mathAverage(): Double {
        return calculateAverage(math)
    }
}
```

- 로컬 함수를 확장하기

```kotlin
class Calculator {
    fun calculateArea(width: Int, height: Int, isRectangle: Boolean): Int {

        fun rectangleArea() = width * height
        fun triangleArea() = width * height / 2

        return if (isRectangle) rectangleArea() else triangleArea()
    }
}

fun main() {
    val calculator = Calculator()

    println("직사각형 면적: ${calculator.calculateArea(10, 5, true)}")
    println("삼각형 면적: ${calculator.calculateArea(10, 5, false)}")
}
```

- `rectangleArea` , `triangleArea` 처럼 내부에 로컬 함수로 넣을 수 있음
- 하지만 내포된 함수의 깊이가 깊어지면 코드를 읽기가 상당히 어려워질 수 있으므로 일반적으로 한 단계만 함수를 내포시키라고 권장함
</details>

<hr>

<details>
<summary><strong>4.1 클래스 계층 정의</strong></summary>

 - 코틀린 가시성/접근 변경자는 자바와 비슷하지만 아무것도 지정하지 않을 경우의 기본 가시성은 다름
- 코틀린에 새로 도입한 `sealed` 변경자를 설명할거임
- `sealed` 는 클래스 상속이나 인터페이스 구현을 제한함

## 4.1.1  코틀린 인터페이스

- 코틀린 인터페이스 안에는 추상 메서드뿐 아니라 구현이 있는 메서드도 정의할 수 있음
- 다만, 인터페이스에는 아무런 상태도 들어갈 수 없음

```kotlin
interface Clickable {
  fun click()
}
```

- 이 코드는 `click` 이라는 추상 메서드가 있는 인터페이스를 정의
- 예를 들어 버튼을 클릭할 . 수있게 만들려면 클래스 선언에서 클래스 이름 뒤에 콜론을 표시하고 그 뒤에 인터페이스 이름을 넣고 `click` 함수의 구현을 제공해야함

```kotlin
class Button: Clickable {
  override fun click() = println("I was clicked")
}

fun main() {
  Button().click()
  // I was clicked
}
```

## 4.1.2 open, final, abstract 변경자: 기본적으로 final

- 기본적으로 코틀린 클래스에 대해 하위 클래스를 만들수 없고, 기반 클래스의 메서드를 하위 클래스가 오버라이드할 수도 없음 → 즉 코틀린에서 모든 클래스와 메서드는 기본적으로 `final` 임
- 자바는 `final` 로 명시적으로 지정하지 않는 . 한모든 클래스를 다른 클래스가 상속할 수 있고, 오버라이드도 가능 → 코틀린은 자바 방식이 편리할 수도 있지만 문제가 될수 있기에 이런 접근 방법을 사용하지 않음

---

- **`취약한 기반 클래스`**라는 문제는 기반 클래스 구현을 변경함으로써 하위 클래스가 잘못된 동작을 하게되는 경우를 뜻함
- 어떤 클래스가 자신을 상속하는 방법에 대해 정확한 규직을 제공하지 않는다면 그 클래스의 클라이언트는 기반 클래스를 작성한 사람의 의도와 다른 방식으로 메서드를 오버라이드할 위험이 있음
- 유명한 책인 이펙티브 자바에서는 “*상속을 위한 설계와 문서를 갖춰라 그럴 수 없다면 상속을 금지하라*” 라는 조언이 있음 ⇒ 이는 특별히 하위 클래스에서 오버라이드하도록 의도된 클래스와 메서드가 아니라면 모두 `final` 로 만들라는 뜻

⇒ 코틀린도 마찬가지로 철학을 따르면서, 클래스와 메서드는 기본적으로 `final` 임

- 어떤 클래스의 상속을 허용하려면 클래스 앞에 `open` 변경자를 붙여야함
- 클래스를 `abstract` 로 선언할 수도 있음, `abstract` 로 선언한 추상 클래스는 인스턴스화 할 수 없음
- 추상 클래스에는 구현이 없어 하위 클래스에서 오버라이드해야만하는 추상 멤버가 있는 것이 보통, 추상 멤버는 항상 열려있음, 따라서 추상 멤버 앞에 `open` 변경자를 명시할 필요 없음

![Image](https://github.com/user-attachments/assets/893014a8-df05-4e6e-ac20-d74367f0d08c)

## 4.1.3 가시성 변경자: 기본적으로 공개

- `가시성 변경자` 는 코드 기반에 있는 선언에 대한 클래스 외부 접근을 제어함
- 코틀린은. `public` `protected` `private` 변경자를 제공
- 코틀린에서 아무 변경자도 없는 선언은 모두 공개, 즉 `public` 임
- 모듈안으로만 한정된 가시성을 위해 코틀린은 `internal` 이라는 가시성을 제공, 모듈은 함께 컴파일되는 코틀린 파일의 집합
- 코틀린에서는 최상위 선언에 대해 `private` 가시성을 허용

![Image](https://github.com/user-attachments/assets/063eff48-eafe-4c08-9b8a-bc25ba1439b7)

## 4.1.4 내부 클래스와 내포된 클래스: 기본적으로 내포 클래스

- 자바처럼 코틀린에서도 클래스 안에 다른 클래스를 선언할 수 있음
- 클래스안에 다른 클래스를 선언하면 도우미 클래스를 캡슐화하거나 코드 정의를 그 코드를 사용하는 곳 가까이에 두고 싶을때 유용
- 하지만 자바와 달리 `nested class(내포 클래스)` 는 명시적으로 요청하지 않는 한 바깥쪽 클래스 인스턴스에 대한 접근 권한이 없음

![Image](https://github.com/user-attachments/assets/d3cab0a4-6200-4f30-a1ec-033dcd6ad401)

## 4.1.5 봉인된 클래스: 확장이 제한된 클래스 계층 정의

- `sealed class(봉인된 클래스)` 는 코틀린에서 클래스 계층의 확장을 제한하기 위해 사용되는 특수한 클래스
- **제한된 상속**  : `sealed class(봉인된 클래스)`는 같은 파일 내에서만 하위 클래스를 정의할 수 있으므로, 미리 정해진 클래스 계층만 존재하게 됨
- **안전한 `when` 표현식 :** 상속 계층이 제한되어 있기 때문에, `when` 식을 사용할 때 모든 경우를 쉽게 확인할 수 있어 컴파일러가 `exhaustive(모든 경우를 처리함을 보장)`검사를 수행할 수 있음
- **추상 클래스와 유사 :**  `sealed class(봉인된 클래스)`는 기본적으로 추상 클래스로 동작하며, 인스턴스를 직접 생성할 수 없음

```kotlin
sealed class Result

data class Success(val data: String) : Result()
data class Error(val message: String) : Result()

fun handleResult(result: Result) {
    when (result) {
        is Success -> println("성공: ${result.data}")
        is Error -> println("오류: ${result.message}")
    }
}
```
</details>


<details>
<summary><strong>4.2 뻔하지 않은 생성자나 프로퍼티를 갖는 클래스 선언 </strong></summary>

 - 객체지향 언어에서 클래스는 보통 생성자를 하나 이상 선언할 수 있음
- 코틀린도 마찬가지지만 한가지 중요하고 특이한 차이가 있음
- 코틀린은 주 생성사와 부 생성자를 구분함
- 또한, 코틀린에서는 초기화 블록을 통해 초기화 로직을 추가할 수 있음

## 4.2.1 클래스 초기화: 주 생성자와 초기화 블록

```kotlin
class User(val nickname: String)
```

- 보통 클래스의 모든 선언은 중괄호({}) 사이에 들어감, 하지만 이 클래스 선언에는 중괄호가 없고 괄호 사이에 `val` 선언만 존재함
- 이렇게 클래스 이름 뒤에 오는 괄호로 둘러싸인 코드를 `주 생성자` 라고 부름
- `주 생성자` 는 생성자 파라미터를 지정하고 그 생성자 파라미터에 의해 초기화되는 프로퍼티를 정의하는 2가지 목적에 쓰임

```kotlin
class User constructor(_nickname: String) {
  val nickname: String
	
  init { // 초기화 블록 
     nickname = _nickname
  }
}
```

- `constructor` 키워드는 주 생성자나 부 생성자 정의를 시작할때 사용
- `init` 키워드는 초기화 블록을 시작함
    - 초기화 블록에는 클래스의 객체가 만들어질 때 실행될 초기화 코드가 들어감
    - 초기화 블록은 주 생성자와 함께 사용
- 생성자 파라미터 `_nickname` 에서 맨 앞의 밑줄(_)은 프로퍼티와 생성자 파라미터를 구분해줌 → 자바에서는 `this.nickname = nickname` 같은 식으로 사용

## 4.2.2 부 생성자: 상위 클래스를 다른 방식으로 초기화

- 일반적으로 코틀린에서는 생성자가 여럿 있는 경우가 자바보다 훨씬 적음
- 코틀린의 디폴트 파라미터 값과 이름 붙은 인자 문법을 사용해 해결할 수 있음
- JAVA
    
    ```kotlin
    public class Downloader {
       public Downloader(String url) {
       // 어떤 코드
       }
       public Downloader(URI uri) {
       // 어떤 코드
       }
    }
    ```
    
- Kotlin
    
    ```kotlin
    open class Downloader {
      constructor(url: String) {
      // 어떤 코드
      }
      constructor(uri: URI) {
      // 어떤 코드
      }
    }
    ```
    
- 이 클래스는 주 생성자를 선언하지 않고 부 생성자만 2가지 선언
- 부 생성자는 `constructor` 키워드로 시작하고, 필요에 따라 얼마든지 많은 부 생성자를 선언해도 됨

## 4.2.3 인터페이스에 선언된 프로퍼티 구현

- 코틀린에서는 인터페이스에 추상 프로퍼치 선언을 넣을 수 있음

```kotlin
interface User {
  val nickname: String 
}
```

- `User` 인터페이스를 구현하는 클래스가 `nickname` 의 값을 얻을 수 있는 방법을 제공해야 한다는 뜻
- 인터페이스는 아무 상태도 포함할 수 없으므로 상태를 저장할 필요가 있다면 인터페이스를 구현한 하위 클래스에서 상태 저장을 위한 프로퍼티 등을 만들어야함

## 4.2.4 게터와 세터에서 뒷받침하는 필드에 접근

- 이제는 이 두 유형을 조합해서 어떤 값을 저장하되 그값을 변경하거나 읽을 때마다 정해진 로직을 실행하는 유형의 프로퍼티를 만드는 방법을 아아보자

```kotlin
class User(val name: String) {
   var address: String = "unspecfied"
      set(value: String) {
          println(
             """
		Address was changed for $name:
		"$field" -> "$value". // <- 뒷받침하는 필드 값 읽기
             """.trimIndent()
          )
          field = value  // <- 뒷받침하는 필드 값 변경하기 
      }
}
```

```kotlin
fun main() {
  val user = User("Alice")
  user.address = "충정로"
  //  Address was changed for Alice : 
  //  "unspecfied" -> "충정로".
}
```

- 코틀린에서 프로퍼티의 값을 바꿀 때는 `user.address = "new value"` 처럼 필드 설정 구문을 사용
- 이 구문은 내부적으로는 `address` 의 `setter` 를 호출

## 4.2.5 접근자의 가시성 변경

- 접근자의 가시성은 기본적으로는 프로퍼티의 가시성과 같음
- 하지만 원한다면 `get` 이나 `set` 앞에 가시성 변경자를 추가해서 접근자의 가시성을 변경할 수 있음

```kotlin
class LengthCounter {
   val counter: Int = 0  // 이 클래스 밖에서 이 프로퍼티의 값을 바꿀 수 없음  
      private set   
	
   fun addWord(word: String) {
      counter += word.length
   }
}
```
</details>


<details>
<summary><strong>4.3 컴파일러가 생성한 메서드: 데이터 클래스와 클래스 위임 </strong></summary>

 - 자바에서는 `equals` , `hashcode` , `toString` 등 비슷한 방식으로 기계적으로 구현할 수 있는 몇가지 메서드가 정의되어 있음
- 코틀린 컴파일러는 한 걸음 더 나가서 이런 메서드를 기계적으로 생성하는 작업을 보이지 않는 곳에서 해줌

---

- 코틀린의 모든 클래스는 기본적으로 최상위 클래스인 **`Any`**를 상속받으며, 이때 자동으로 다음의 세 가지 메서드가 제공
- **`equals(other: Any?)`**
    - 기본적으로 참조(주소) 동등성 비교를 수행
    - 객체의 내용에 기반한 동등성 비교가 필요하다면 재정의가 필요
- **`hashCode()`**
    - 객체의 해시 코드를 반환하며, equals()와의 일관성을 유지
    - `equals()`를 재정의하는 경우, 반드시 `hashCode()`도 같이 재정의해야 함
- **`toString()`**
    - 기본 구현은 클래스 이름과 해시 코드를 포함한 문자열을 반환
    - 디버깅이나 로깅 목적으로 객체의 상태를 명확히 표현하도록 재정의할 수 있음

---

- **데이터 클래스**의 경우, 위의 세 메서드 외에도 프로퍼티 기반의 copy()와 componentN() 메서드가 자동으로 생성되어, 객체 비교와 복사, 구조 분해 선언이 용이해짐

---

- 클래스 위임 : by 키워드 사용
    - 클래스 위임은 특정 인터페이스의 구현을 다른 객체에게 위임하는 패턴
    - 이를 위해 Kotlin에서는 by 키워드를 사용
    - 예를 들어, 어떤 클래스가 인터페이스를 구현할 때, 실제 구현은 다른 객체에 맡기고 호출은 자동으로 해당 객체의 메서드가 실행되도록 할 수 있음
</details>


<details>
<summary><strong>4.4 object 키워드: 클래스 선언과 인스턴스 생성을 한꺼번에 하기</strong></summary>

 
- 코틀린에서는 `object` 키워드가 몇 가지 상황에서 쓰임
- 객체 선언
    - `싱글턴` 을 정의하는 한 가지 방법
- 동반 객체
    - 어떤 클래스와 관련이 있지만 호출하기 위해 그 클래스의 객체가 필요하지는 않은 메서드와 팩토리 메서드를 담을 때 쓰임
    - 동반 객체의 멤버에 접근할 때는 동반 객체가 포함된 클래스의 이름을 사용
- 객체 식 : 자바의 익명 내부 클래스 대신 쓰임

## 4.4.1 객체 선언 : 싱글턴을 쉽게 만들기

- 객체지향 시스템을 설계하다 보면 인스턴스가 하나만 필요한 클래스가 유용한 경우가 많음
- 자바에서는 보통 클래스의 생성자를 `private` 으로 제한하고 정적인 필드에 . 그클래스의 유일한 객체를 저장하는 `싱글턴 패턴` 을 통해 이를 구현함
- 코틀린은 객체 선언 기능을 통해 `싱글턴` 을 언어에서 기본 지원함
    
    ```kotlin
    object Payroll {
    	fun test() {
    		// 
    	}
    }
    ```
    
- 객체 선언은 `object` 키워드로 시작
- 객체 선언에서는 생성자를 쓸 수 없음 → 이유는 일반 클래스 인스턴스와 달리 싱글턴 객체는 객체 선언문이 있는 위치에서 생성자 호출없이 즉시 만들어짐

## 4.4.2 동반 객체: 팩토리 메서드와 정적 멤버가 들어갈 장소

- 코틀린 클래스 안에는 정적인 멤버가 없음
- 코틀린 언어는 자바 `static` 키워드를 지원하지 않음, 그 대신 코틀린에서는 패키지 수준의 최상위 함수와 객체 선언을 활용함
- 대부분의 경우 최상위 함수를 활용하는 편을 더 권장함

## 4.4.3 동반 객체를 일반 객체처럼 사용

- 동반 객체는 클래스 안에 정의된 일반 객체
- 따라서 다른 객체 선언처럼 동반 객체에 이름을 붙이거나, 동반 객체가 인터페이스를 상속하거나, 동반객체 안에 확장 함수와 프로퍼티를 정의할 수 없음

```kotlin
// 1. 인터페이스 정의: 동반 객체가 구현할 인터페이스
interface Factory<T> {
    fun create(): T
}

// 2. Person 클래스 정의와 동반 객체 구현
class Person(val name: String) {
    // 동반 객체가 Factory<Person> 인터페이스를 구현함
    companion object : Factory<Person> {
        override fun create(): Person = Person("Default Name")
    }
}

// 3. 동반 객체에 대한 확장 함수 정의
fun Person.Companion.greet() {
    println("Hello from the Person companion object!")
}

// 4. 동반 객체를 일반 객체처럼 매개변수로 전달하는 함수
fun <T> build(factory: Factory<T>): T = factory.create()

fun main() {
    // 동반 객체의 메서드를 직접 호출하여 객체 생성
    val person1 = Person.create()
    println("person1.name = ${person1.name}")

    // 동반 객체에 정의된 확장 함수 호출
    Person.greet()

    // 동반 객체를 일반 객체처럼 함수의 인자로 전달하여 사용
    val person2 = build(Person)
   }
```

## 4.4.4 객체 식: 익명 내부 클래스를 다른 방식으로 작성

- `object` 키워드를 싱글턴과 같은 객체를 정의하고 그 객체에 이름을 붙일 때만 사용하지 않음
- 익명 객체를 정의할 때도 `object` 키워드를 씀	
</details>


<details>
<summary><strong>4.5 부가 비용 없이 타입 안전성 추가: 인라인 클래스</strong></summary>
인라인 클래스를 사용하면 수명이 짧은 객체를 많이 할당함으로써 발생할 수있는 겅능 저하를 피하면서도 프로그램에 새로운 타입 안정성 계층을 추가할 수있음 
</details>

<hr>
<details>
<summary><strong>5.1 람다식과 멤버 참조 </strong></summary>
	- 자바 프로그래머들은 람다의 도입을 오랫동안 기다려왔고 자바8의 람다는 . 그기다림의 끝
- 람다가 왜 중요할까?

## 5.1.1 람다 소개: 코드 블록을 값으로 다루기

- 람다는 **코드 블록을 변수에 담거나** **함수 인자로 넘길 수 있음**
- 함수형 프로그래밍의 핵심 개념 중 하나

```kotlin
val greet = { println("Hello!") }
greet()  // Hello! 출력

//함수처럼 변수 greet를 호출할 수 있음.
```

## 5.1.2 람다와 컬렉션

- 컬렉션 함수(filter, map, forEach 등)와 **람다를 조합하면 강력해짐**
- 반복문 없이 **짧고 읽기 쉬운 코드**를 만들 수 있음

## 5.1.3 람다식의 문법

- { 매개변수 -> 본문 } 형태
- 매개변수가 하나일 땐 it 사용 가능
- 타입 생략 가능(컴파일러가 추론)

```kotlin
val square: (Int) -> Int = { it * it }
println(square(4))  // 16
```

## 5.1.4 현재 영역에 있는 변수 접근

- 람다는 **바깥 스코프**에 있는 변수를 자유롭게 참조할 수 있음  (→ **클로저**)
- 값이 변경될 수도 있음

```kotlin
var counter = 0
val increment = { counter++ }
```

## 5.1.5 멤버 참조

- 클래스명::함수명, 객체명::함수명 형태로 사용
- 람다를 더 짧고 깔끔하게 표현할 수 있음

## 5.1.6 값과 엮인 호출 가능

- 객체에 묶인(바인딩된) 멤버 참조를 만들 수 있음
- 이후에 이 참조를 호출할 때마다 **묶인 값**을 기준으로 동작함

```kotlin
val number = 42
val isEqualTo42 = number::equals

println(isEqualTo42(42))  // true
println(isEqualTo42(100)) // false
```
</details>

<details>
<summary><strong>5.2 자바의 함수형 인터페이스 사용: 단일 추상 메서드 </strong></summary>
	- JVM 생태계에는 이미 코틀린으로 작성된 수많은 라이브러리가 있고, 이런 라이브러리는 코틀린 람다를 직접 사용할 수 있음
- 하지만 코틀린 프로젝트에 자바로 작성한 라이브러리를 사용하게 될 가능성이 큼, 다행인 점은 코틀린 람다가 자바 API와 완전히 호환된다는 점

## 5.2.1 람다를 자바 메서드의 파라미터로 전달

- 자바 메서드가 **함수형 인터페이스**를 받으면, 코틀린에서는 **람다식**을 그냥 넘기면 됨

```java
public interface Comparator<T> {
    int compare(T o1, T o2);
}
```

```java
val list = listOf(3, 5, 1, 2)
val sortedList = list.sortedWith { a, b -> a - b }

println(sortedList) // [1, 2, 3, 5]
```

- sortedWith 안에 **람다**를 넣었지만, 사실 이건 **Comparator**를 자동으로 만들어서 넘긴 거임

## 5.2.2 SAM 변환: 람다를 함수형 인터페이스로 명시적 변환

- SAM(Single Abstract Method) 변환이란?
    - **추상 메서드가 딱 하나만 있는 인터페이스**를 코틀린 람다로 자동 변환하는 것.
- 대표적인 예 : `Runnable`, `Callable`, `Comparator`, `ActionListener`, `Predicate` 등

- **SAM 변환이 가능한 경우**
    - **인터페이스**여야 함. (클래스 아님)
    - **추상 메서드가 딱 하나**여야 함.
- **SAM 변환이 안 되는 경우**
    - 메서드가 2개 이상이면 **람다로 변환할 수 없음**.
</details>

<details>
<summary><strong>5.3 코틀린에서 SAM 인터페이스 정의: fun interface</strong></summary>

- 코틀린에서도 자바처럼 “추상 메서드 하나만 있는 인터페이스(SAM 인터페이스)“를 만들 수 있음
- 이때 사용하는 키워드는 바로 `fun interface`
- `fun interface`로 선언하면, 람다식으로 인스턴스를 정의 할 수 있음

```kotlin
fun interface MyFunction {
    fun invoke(x: Int): Int
}
```

```kotlin
val double = MyFunction { it * 2 }
println(double.invoke(3)) // 6 <= 이렇게 호출 
```
</details>

<details>
<summary><strong>5.4 수신 객체 지정 람다 : with, apply, also </strong></summary>
	
## 5.4.1 with 함수

- 많은 언어가 어떤 객체의 이름을 반복하지 않고도 그 객체에 대해 다양한 연산을 수행하는 기능을 제공
- 블록 내에서는 객체의 프로퍼티나 메서드를 직접 호출할 수 있어 코드가 간결해짐
- 블록의 마지막 표현식 결과를 반환하므로, 특정 작업의 결과값을 얻을 때 유용함

```kotlin
data class Person(var name: String, var age: Int)

fun main() {
    val person = Person("Alice", 25)
    // with 함수를 사용하여 여러 작업을 수행하고 결과값을 반환
    val description = with(person) {
        // 블록 내에서는 person 객체의 속성을 직접 참조할 수 있음
        "Name: $name, Age: $age"
    }
    println(description) // Name: Alice, Age: 25
}
```

## 5.4.2 apply 함수

- `apply` 함수느 거의 `with` 와 동일하게 작동
- 람다 블록 내부에서 객체의 프로퍼티나 메서드에 직접 접근할 수 있음(즉, 수신 객체로 처리됨).
- 블록의 결과와 상관없이 항상 원래의 객체 자신을 반환함
- 객체의 초기화나 설정 시에 매우 유용함

```kotlin
data class Person(var name: String = "", var age: Int = 0)

fun main() {
    // apply를 사용하여 객체를 초기화
    val person = Person().apply {
        name = "Bob"
        age = 30
    }
    // apply는 항상 원래 객체를 반환하므로 person은 변경된 객체
    println(person) // Person(name=Bob, age=30)
}
```

## 5.4.3 객체에 추가 작업 수행: also

- 전달된 객체가 블록 내에서 it로 전달됨
- 주로 사이드 이펙트 작업(예: 디버깅, 로깅 등)을 수행할 때 사용되며, 최종적으로 원본 객체를 그대로 반환함
- 객체의 값이나 상태를 변경하지 않고 부가적인 작업을 수행할 때 유용함

```kotlin
fun main() {
    // also를 사용하여 부가 작업을 수행
    val numbers = mutableListOf("One", "Two", "Three").also {
        println("초기 리스트: $it")
        //  로깅이나 디버그 용도로 활용 가능
    }
    // numbers는 리스트 그 자체로 반환됨
    println("최종 리스트: $numbers")
}
```
</details>
<hr>
<details>
<summary><strong>6.1 컬렉션에 대한 함수형 API</strong></summary>
- 함수형 프로그래밍 스타일은 컬렉션을 다룰 때 여러 가지 장점을 제공

## 6.1.1 원소 제거와 변환: filter 와 map

- `filter` 함수는 컬렉션을 순회하면서 주어진 람다가 `true` 를 반환하는 원소들만 모음
- 예를 들어 리스트가 있다면 `filter` 를 통해 그중에서 짝수만 골라 낼 수 있음

```kotlin
fun main() {
	val list = listOf(1,2,3,4)
	println(list.filter{ it % 2 == 0})
	// [2, 4]
}
```

- `filter` 함수는 주어진 술어와 일치하는 원소들로 이뤄진 새 컬렉션을 만들 . 수있지만 그 과정에서 원소를 변환하지 않음

- `map` 함수는 입력 컬렉션의 우너소를 변활 할 수 있게 해줌
- `map` 은 주어진 함수를 컬렉션의 각 원소에 적용하고 그 결과값들을 새 컬렉션에 모아줌

```kotlin
fun main() {
	val list = listOf(1,2,3,4)
	println(list.map{ it * it})
	// [1, 4, 9, 16]
}
```

## 6.1.2 컬렉션 값 누적: reduce와 fold

- `reduce` 를 사용하면 컬렉션의 첫 번째 값을 누적기에 넣음

```kotlin
val numbers = listOf(1, 2, 3, 4)
val sum = numbers.reduce { acc, i -> acc + i } //  10
```

- `fold` 함수는 개념적으로 `reduce` 와 비슷하지만 컬렉션 첫 번째 원소를 누적 값으로 시작하는 대신, 임의의 시작 값을 선택할 수 있음

```kotlin
val numbers = listOf(1, 2, 3, 4)
val sum = numbers.fold(0) { acc, i -> acc + i } //  10
```

- **컬렉션이 비어있는 경우**: `reduce`는 비어있는 경우 예외를 던지므로, 비어있을 가능성이 있다면 fold를 사용하거나 미리 검사를 해야 함
- **누적 로직의 복잡성**: 누적 연산의 결과 타입이 요소 타입과 다를 때는 `fold`가 더 유연하게 사용할 수 있음
- **함수형 프로그래밍 스타일**: 이들 함수는 코드의 간결성과 가독성을 높이며, 명령형 반복문보다 함수형 스타일을 선호하는 경우 유용함

## 6.1.3 컬렉션에 술어 적용: all, any, none, count, find

- `all`
    - 모든 요소가 주어진 조건을 만족하는지 확인함
    
    ```kotlin
    val numbers = listOf(2, 4, 6)
    val areAllEven = numbers.all { it % 2 == 0 }  // true
    ```
    

- **`any`**
    - **컬렉션 내에서 하나 이상의 요소가 조건을 만족하는지 검사함**
    
    ```kotlin
    val numbers = listOf(1, 3, 5, 6)
    val hasEvenNumber = numbers.any { it % 2 == 0 }  //true
    ```
    

- **`none`**
    - 컬렉션 내의 어떤 요소도 주어진 조건을 만족하지 않는지 확인함
        
        ```kotlin
        val numbers = listOf(1, 3, 5)
        val hasNoEvenNumber = numbers.none { it % 2 == 0 }  // true
        ```
        

- **`count`**
    - ****조건을 만족하는 요소의 개수를 계산함
    
    ```kotlin
    val numbers = listOf(1, 2, 3, 4, 5)
    val evenCount = numbers.count { it % 2 == 0 }  //  2
    ```
    

- **`find`**
    - 주어진 조건에 처음으로 부합하는 요소를 검색하여 반환함
    - 조건을 만족하는 첫 번째 요소를 찾으며, 만족하는 요소가 없으면 `null`을 반환함
    
    ```kotlin
    val numbers = listOf(1, 3, 5, 7)
    val found = numbers.find { it > 4 }  //  5/
    ```
    

## 6.1.4 리스트를 분할해 리스트의 쌍으로 만들기: partition

- 반환 타입은 `Pair<List<T>`, `List<T>>`
- 리스트를 **둘로 나눠야 할 때 간결하고 가독성이 좋은 방법**
- `filter` 두 번 쓰는 것보다 효율적임

```kotlin
val numbers = listOf(1, 2, 3, 4, 5, 6)
val (even, odd) = numbers.partition { it % 2 == 0 }

println(even) // [2, 4, 6]
println(odd)  // [1, 3, 5]
```

## 6.1.5 리스트를 여러 그룹으로 이뤄진 맵으로 바꾸기: groupBy

- `groupBy`는 리스트를 **조건 기반으로 맵으로 변환**할 때 사용
- 반환값은 `Map<K, List<V>>`
- 조건 함수의 결과가 **키**가 되며, 키에 해당하는 요소들이 리스트로 묶임
- 복잡한 필터/분류 작업을 깔끔하게 처리 가능

```kotlin
val words = listOf("a", "ab", "abc", "de", "def")
val grouped = words.groupBy { it.length }

println(grouped)
// {1=[a], 2=[ab, de], 3=[abc, def]}
```

## 6.1.6 컬렉션을 맵으로 변환: associate, associateWith, associateBy

- `associate`, `associateWith`, `associateBy`는 컬렉션을 **`Map`으로 변환**할 때 사용함
- 각 함수는 어떤 값을 **`Map`의 키, 값으로 삼을지**에 따라 역할이 다름
- `associate`
    - **각 원소를 (key to value) 쌍으로 바꿔서 Map 생성**
    - `associate { element -> key to value }`
        
        ```kotlin
        val words = listOf("a", "ab", "abc")
        val result = words.associate { it to it.length }
        // {a=1, ab=2, abc=3}
        ```
        
- `associateWith`
    - **리스트의 원소를 `Map`의 키로 사용하고**, 주어진 식의 결과를 값으로 사용
    - `associateWith { value }`
    
    ```kotlin
    val words = listOf("a", "ab", "abc")
    val result = words.associateWith { it.length }
    // {a=1, ab=2, abc=3}
    ```
    
- `associateBy`
    - **리스트의 원소를 `Map`의 값으로 사용하고**, 주어진 식의 결과를 키로 사용
    - `associateBy { key }` 또는 `associateBy({ key }) { value }`
    
    ```kotlin
    val words = listOf("a", "ab", "abc")
    val result = words.associateBy { it.length }
    // {1=a, 2=ab, 3=abc}
    
    val result2 = words.associateBy({ it.length }) { it.uppercase() }
    // {1=A, 2=AB, 3=ABC}
    ```
    

## 6.1.7 가변 컬렉션의 원소 변경: replaceAll, fill

- `replaceAll`
    - 리스트의 **각 원소에 대해 변환 함수를 적용**해서, 그 결과로 **원소를 교체**
    - Java의 `List.replaceAll`과 유사
    
    ```kotlin
    val list = mutableListOf("a", "b", "c")
    list.replaceAll { it.uppercase() }
    
    println(list) // [A, B, C]
    ```
    
- `fill`
    - 리스트의 **모든 원소를 동일한 값으로 설정**
    
    ```kotlin
    val list = MutableList(5) { 0 }
    list.fill(42)
    
    println(list) // [42, 42, 42, 42, 42]
    ```
    

## 6.1.8 컬렉션의 특별한 경우 처리: ifEmpty

- `ifEmpty` 함수는 컬렉션이 비어 있을 때 대체 동작을 지정할 수 있는 함수
- 주로 비어 있을 경우 기본값을 제공하거나, 다른 로직으로 전환할 때 유용하게 사용

```kotlin
val names = listOf<String>()
val defaultNames = names.ifEmpty { listOf("Default") }

println(defaultNames) // [Default]
```

## 6.1.9 컬렉션 나누기: chunked와 windowed

- `chunked(n)`
    - 컬렉션을 고정 크기의 청크(조각)로 나눔
    - 마지막 조각은 부족한 크기일 수 있음
        
        ```kotlin
        val result = (1..10).toList().chunked(3)
        println(result) // [[1, 2, 3], [4, 5, 6], [7, 8, 9], [10]]
        ```
        
- `windowed(n, step, partialWindows = true)`
    - 지정한 크기와 간격으로 **슬라이딩 윈도우** 형태로 분할
    - `partialWindows = false` 면 마지막 불완전 윈도우는 제거됨
    
    ```kotlin
    val result = (1..5).toList().windowed(3)
    println(result) // [[1, 2, 3], [2, 3, 4], [3, 4, 5]]
    ```
    

## 6.1.10 컬렉션 합치기: zip

- 두 컬렉션을 쌍(pair)으로 묶어줌 (`Pair<A, B>`)
- 길이가 다르면 짧은 쪽에 맞춰서 잘림

```kotlin
val letters = listOf("a", "b", "c")
val numbers = listOf(1, 2, 3)

val result = letters.zip(numbers)
println(result) // [(a, 1), (b, 2), (c, 3)]
```

## 6.1.11 내포된 컬렉션의 원소 처리: flatMap과 faltten

- `flatten()`
    - 중첩된 컬렉션을 한 단계 평탄화(flatten) 함
    
    ```kotlin
    val list = listOf(listOf(1, 2), listOf(3, 4))
    val result = list.flatten()
    // [1, 2, 3, 4]
    ```
    
- `flatMap()`
    - 각 원소에 대해 리스트를 반환하고, 결과를 한 리스트로 합침
    
    ```kotlin
    val list = listOf("abc", "def")
    val result = list.flatMap { it.toList() }
    // ['a', 'b', 'c', 'd', 'e', 'f']
    ```
</details>

<details>
<summary><strong>6.2 지연 계산 컬렉션 연산: 시퀀스 </strong></summary>
	
- Sequence는 **지연(lazy) 계산 방식**으로 작동하는 컬렉션 처리 방식
- 일반 컬렉션은 각 연산마다 **중간 결과를 새 컬렉션에 저장**하지만
- Sequence는 **필요할 때마다 원소를 계산**함 → **메모리 낭비 줄고 속도 개선 가능**
    

```kotlin
val list = listOf(1, 2, 3, 4, 5)
val seq = list.asSequence()
     .filter { 
	println("filter $it"); 
	it % 2 == 0 
     }
     .map {
	println("map $it"); 
	it * 2 
     }

println(seq.toList())
// filter 1, filter 2, map 2, filter 3, filter 4, map 4, filter 5
```
</details>
<hr>
<details>
<summary><strong>7.1 NullPointerException을 피하고 값이 없는 경우 처리: 널 가능성</strong></summary>
	
- 널 가능성은 `NullPointerException` 오류를 피할 수 있게 돕는 코틀린 타입 시스템의 특성임
- 코틀린을 포함한 최신 언어에서 null에 대한 접근 방법은 가능한 이 문제를 실행 시점에서 컴파일 시점으로 옮기는 것
</details>
<details>
<summary><strong>7.2 널이 될 수 있는 타입으로 널이 될 수 있는 변수 명시</strong></summary>
- Nullable 타입 선언
    - 기본적으로 코틀린의 모든 참조 타입은 non‑null.
    - `null` 값을 들고 싶다면 타입 이름 뒤에 ?를 붙여야 함
    
```kotlin
var nonNull: String = "Hello"
var nullable: String? = "안녕"  // nullable 변수
nullable = null                // OK
nonNull = null      
```
    
- 타입 추론 시 주의점
    - 초기값이 `null` 하나뿐인 경우, 컴파일러가 타입을 추론할 수 없어 오류 발생
    
```kotlin
var inferred = null   // 오류: 타입 추론 불가
var inferred: String? = null  // OK 
```
</details>
