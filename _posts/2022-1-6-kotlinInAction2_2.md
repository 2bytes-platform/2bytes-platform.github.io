---
layout: post
title: "📅 Kotlin in Action - 2장 ②"
excerpt: "Kotlin in Action 2장 요약 노트입니다."
subtitle: "Kotlin in Action"
toc: true
toc_sticky: true
toc_label: "페이지 주요 목차"
date: 2022-1-6
tags: [Kotlin]
---

#### 2.2.3 코틀린 소스코드 구조: 디렉토리와 패키지

- 코틀린은 node.js 처럼 모듈화로 관리할 수 있고 이를 **패키지**라고 함. 그리고 이 패키지 안에는 클래스, 함수, 프로퍼티
등이 있으며, 자유롭게 꺼내 쓸 수 있음  

- 프로젝트에서 자바와 혼용할 경우, 자바와 같이 패키지 별로 디렉터리를 구성하자

```kotlin
package geometry.shapes // 패키지 선언
import java.util.Random // 표준 자바 라이브러리 클래스를 import
class Rectangle(val height: Int, val width: Int) {
    val isSquare: Boolean
        get() = height = width
}
fun createRandomRectangle(): Rectangle {
    val random = Random()
    return Retangle(random.nextInt(), random.nextInt())
}
```

```
pakage.* // 패키지 안의 모든 클래스, 함수, 프로퍼티까지 다 불러옴
package geometry.example
import geometry.shapes.createRandomRectangle // 이름으로 함수 import
fun main(args: Array<String>) {
    println(createRandomRectangle().isSquare)
}
```
### 2.3 선택 표현과 처리: enum과 when
#### 2.3.1 선택 표현과 처리 - enum 클래스 정의

>enum - 복수의 요소를 나열한다는 점에서 JS의 배열과 유사하지만 프로퍼티나 메소드까지 정의 가능
```kotlin
enum class Color (
    val r: Int, val g: Int, val b: Int // 상수 프로퍼티 정의
) {
    RED(255,0,0), ORANGE(255, 165, 0), // 상수 생성 시 이에 대한 프로퍼티 값 지정
    YELLOW(255, 255, 0), GREEN(0, 255, 0), BLUE(0, 255, 255); // 반드시 !세미콜론으로 마물
    
    fun rgb() = (r * 256 + g) * 256 + b // enum 클래스 안에서 메소드를 정의
}
```
- enum에 생성자와 프로퍼티를 선언하고 클래스 안에 메소드를 정의하는 경우 반드시 상수 목록과 메소드 정의 사이에 세미콜론

#### 2.3.2 / 2.3.3 when으로 enum 클래스 다루기

- 분기를 생성하여 해당 조건에 맞는 값을 반환해주는 강력한 기능을 보유. 자바의 switch와 동일하나, 분기 조건에 상수만
사용할 수 있는 swith와 달리 when의 분기 조건은 임의의 객체를 허용
```kotlin
// when 분기 조건에 여러 값 사용하기
fun getWarmth (color: Color) = when (color) {
    Color.RED, Color.ORANGE, Color.YELLOW -> "warm"
    Color.GREEN -> "neutral"
    Color.BLUE, Color.INDIGO, Color.VIOLET -> "cold"
}
println(getWarmth(Color.ORANGE)) // warm

// when 분기 조건에 여러 다른 객체 사용하기
fun mix(c1: Color, c2: Color) = 
    when (setof(c1,c2)) {
        setOf(RED, YELLOW) -> ORANGE 
        setOf(YELLOW, BLUE) -> GREEN
        setOf(BLUE, VOILET) -> INDIGO
        else -> throw Exception("FUCKED")
    }

println(mix(BLUE, YELLOW)) // GREEN
```

- setOf 함수는 인자로 전달받은 여러 객체를 포함하는 집합인 set 객체로 만들어 줌. 집합(set)은 원소가 모여있는 컬렉션으로
순서는 상관없음

#### 2.3.4 인자없는 when 사용

- 앞 전의 함수는 호출될 떄마다 여러 Set 인스턴스를 생성하기 때문에 비효율성이 발생. 이에 다음과 같이 인자가 없는 when 식을
사용하면 불필요한 객체(=가비지 객체) 생성을 막을 수 있음

```kotlin
fun mixOptimized(c1: Color, c2: Color) = 
    when {
        (c1 == RED && c2 == YELLOW) || (c1 == YELLOW && c2 == RED) -> ORANGE
        (c1 == YELLOW && c2 == BLUE) || (c1 == BLUE && c2 == YELLOW) -> GREEN
        (c1 == BLUE && c2 == VIOLET) || (c1 == VIOLET && c2 == BLUE) -> INDIGO
        
        else -> throw Exception("FUCKED")
    }

println(mixOptimized()(BLUE, YELLOW)) // GREEN

// 
fun main() {
	println(doWhen(1))
}

fun doWhen (a: Any): String { // 출력값 타입을 지정하지 않은 경우 Type mismatch: inferred type is String but Unit was expected
	var result = when(a) {
		1 -> "1"
		"Sasha" -> "사샤"
		else -> "유효한 값을 입력하십시오"
	}
	return result
}

```

#### 2.3.5 스마트 캐스트: 타입 검사와 타입 캐스를 조합 - 보류 
- 스마트캐스트: 굳이 변수를 원하는  타입으로 캐스팅하지 않아도 마치 처음부터 그 변수가 원하는 타입으로 선언된 것처럼
사용할 수 있는데, 이를 컴파일러가 자동으로 수행해주는 것.

```kotlin
interface Expr
class Num(val value: Int) : Expr
class Sum(val left: Expr, val right: Expr) : Expr
```

#### 2.3.6 리팩토링: if를 when으로 변경

if 식을 이용한 값 생성 
```kotlin
fun eval(e: Expr): Int = 
    if (e is Num) {
        e.value
    } else if (e is Sum) {
        eval(e.right) + eval(e.left)
    } else {
        throw IllegalArgumentException("Unknown expression")
    }
println(eval(Sum(Num(1), Num(2)))) // 3
```
if 대신에 when을 사용해서 좀 더 다듬어보자
```kotlin
fun eval(e: Expr) : Int = 
    when (e) {
        is Num -> // 인자 타입을 검사한다 
            e.value
        is Sum -> 
            eval(e.right) + eval(e.left)
    else ->         
        throw IllegalArgumentException("Unknown expression")
    }
```
if나 when의 각 분기에서 수행해야 하는 로직이 복잡해지면 분기 본문에 블록 사용 가능  

#### 2.3.7 if와 when의 분기에서 블록 사용

if나 when 모두 분기에 블록 사용이 가능하며, 그런 경우 블록의 가장 마지막 문장이 블록의 전체 결과가 됨. return을 
따로 써줄 필요가 없음.
```kotlin
fun evalWithLogging(e: Expr) : Int = 
    when (e) {
        is Num -> {
            println("num: ${e.value}")
            e.value
        }
        is Sum -> {
            val left = evalWithLogging(e.left)
            val right = evalWithLogging(e.right)
            println("sum: ${left} + ${right}")
            left + right
        }
        else -> throw IllegalArgumentException("Unknown expression")
    }
```
