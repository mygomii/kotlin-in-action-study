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
  - while은 다른 언어와 마찬가지인 전통적인 형식을 따름

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
