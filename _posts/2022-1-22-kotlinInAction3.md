---
layout: post
title: "📅 Kotlin in Action - 3장 함수 정의와 호출"
excerpt: "Kotlin in Action 3장 요약 노트입니다."
subtitle: "Kotlin in Action"
toc: true
toc_sticky: true
toc_label: "페이지 주요 목차"
date: 2022-1-22
tags: [Kotlin]
---

### 3.1 코틀린에서 컬렉션 만들기

- 코틀린에서는 자체 컬렉션을 제공하지 않음. 표준 자바 컬렉션을 활용하면 기존 자바 코드와 상호작용하기가 쉽기 때문

```kotlin
// 코틀린은 자바보다 더 많은 컬렉션 기능을 쓸 수 있음
val strings = listOf("first", "second", "third")
println(strings.last()) // third
val numbers = setOf(1, 14, 2)
println(numbers.max()) // 14
```

### 3.2 함수를 호출하기 쉽게 만들기

- 원소 사이를 세미콜론으로 구분하고 괄호로 리스트를 둘러싸는 함수를 다음과 같이 생성
- 함수를 호출 joinToString(list, "; ", "(", ")")을 간략하게 나타내보자
```kotlin
fun main() {
	val list = listOf(1,2,3)
    println(joinToString(list, "; ", "(", ")"))
}

fun <T> joinToString(
	collection: Collection<T>,
    separator: String,
    prefix: String,
	postfix: String
): String {
    
    val result = StringBuilder(prefix)
    for((idx, ele) in collection.withIndex()) {
        if (idx > 0) result.append(separator)
        result.append(ele)
    }
    result.append(postfix)
    return result.toString()
}
```

#### 3.2.1 이름 붙인 인자

- 코틀린으로 작성한 함수를 호출할 때는 아래 스니펫과 같이 전달 인자의 이름을 명시할 수 있음
- 자바로 작성한 코드를 호출 시, 인식 문제로 인해 이름 붙인 인자를 사용할 수 없음

```kotlin
joinToString(list, separator = "; ", prefix = "(", postfix = ")")
```

#### 3.2.2 디폴트 파라미터 값

- 코틀린은 함수 선언에서 인자의 default 값을 지정하여 너무 많은 메소드 오버로딩을 피할 수 있음
- 함수를 선언할 때와 같은 순서로 인자를 지정

```kotlin
joinToString(list, ",", "", "")
joinToString(list) // separator, prefix, postfix 생략
joinToString(list, "; ") // separator = ": "로 지정, prefix & postfix 생략
```

>자바에는 default 인자값이라는 개념이 없어서 코틀린 함수를 자바에서 호출하는 경우에는 모든 인자 명시 필요!

#### 3.2.3 정적인 유틸리티 클래스 없애기: 최상위 함수와 프로퍼티

- 다양한 정적 메소드를 모아두기만 하고, 특별한 상태나 인스턴스 메소드는 없는 클래스 ex) JDK collections 클래스
- API 생성 시, 재활용하고 싶은 로직들을 따로 모아두는 작업을 생각하자

```kotlin
// 생성된 join.kt 파일 내 joinToString() 함수를 최상위 함수로 선언
package strings
fun joinToString(): String {}
```
```kotlin
// 코틀린 최상위 함수가 포함되는 클래스의 이름을 바꾸고 싶다면 파일에 @JvmName Annotation 추가
@file: JvmName("StringFunctions")
package strings
fun joinToString():String{}

```

- 함수와 마찬가지로 프로퍼티도 파일의 최상위 수준에 놓을 수 있으며, 해당 값은 정적 필드에 저장
```kotlin
var opCount = 0
fun performOperation() {
    opCount++
}
fun reportOperationCount() {
    println("Operation performed $opCount times")
}
```

### 3.3 메소드를 다른 클래스에 추가: 확장 함수와 확장 프로퍼티

- 확장 함수: 기존 자바 API를 재작성하지 않고, 코틀린이 제공하는 매서드를 이용할 수 있게 만들어 줌. 즉, 어떤 클래스의 멤버
메서드인 것처럼 호출 가능하지만 그 클래스 밖에 선언된 함수

```kotlin
package strings
fun String.lastChar(): Char = get(length - 1) // this 생략 가능
/**
 * receiver type(수신 객체 타입): 함수가 확장할 클래스의 이름
 * receiver object(수신 객체): 확장 함수가 호출되는 대상이 되는 값(객체)
 */
```

#### 3.3.1 import와 확장 함수

```kotlin
import strings.lastChar
import strings.*
val c = "Kotlin".lastChar()

import strings.lastChar as last
val c = "Kotlin".last()
```

#### 3.3.3 확장 함수로 유틸리티 함수 정의

```kotlin
fun main() {
    val list = listOf(1,2,3)
    println(joinToString(list, "; ", "(", ")"))
}
fun <T> collection<T> join,ToString (
    separator: String = ", "
    prefix: String = "",
    postfix: String = ""
): String {

    val result = StringBuilder(prefix)
    for((idx, ele) in collection.withIndex()) {
        if (idx > 0) result.append(separator)
        result.append(ele)
    }
    result.append(postfix)
    return result.toString()
}
```

#### 3.3.4 확장 함수는 오버라이드 불가

```kotlin
fun main() {
    val view: View = Button()
    view.click() // Button clicked -> 오버라이드o 
    view.showOff() // Sasha -> 오버라이드x
}

open class View {
    open fun click() = println("View clicked")
}
class Button: View() {
    override fun click() = println("Button clicked")
}
fun View.showOff() = println("Sasha")
fun Button.showOff() = println("Lisa")

``` 
> dynamic dispatch (동적 디스패치): **실행** 시점에 객체 타입에 따라 동적으로 호출될 대상 메소드를 결정하는 방식  
> static dispatch (정적 디스패치): **컴파일** 시점에 알려진 변수 타입에 따라 정해진 메서드를 호출하는 방식


#### 3.3.5 확장 프로퍼티

- 기존 클래스 객체에 대한 프로퍼티 형식의 구문으로 사용할 수 있는 API를 추가

```kotlin
// 확장 프로퍼티 선언
val StringBuilder.lastChar: Char
get() = get(length - 1) // 프로퍼티 게터
set(value: Char) {
	this.setCharAt(length - 1. value) // 프로퍼티 세터
}
```

### 3.4 컬렉션 처리: 가변 길이 인자, 중위 함수 호출, 라이브러리 지원

- vararg 키워드 사용 및 호출 시, 인자 개수가 달리질 수 있는 함수를 정의
- infix(중위) 함수 호출 구문 사용 시, 하나의 인자를 갖는 메소드를 간편하게 호출
- destructuring declaration(구조 분해 선언) 사용 시, 복합적인 값을 분해해서 다수의 변수에 할당 가능

#### 3.4.2 가변 인자 함수: 인자의 개수가 달라질 수 있는 함수 정의

- 가변 길이 인자: 메소드를 호출할 때 원하는 개수만큼 값을 인자로 넘기면 자바 컴파일러가 배열에 그 값들을 넣어주는 기능
- 스프레드 연산자: 배열 앞에 *를 붙여주면 이용 가능. 그러나 자바에서 사용 불가
```kotlin
fun main(args: Array<String>) {
	val list = listOf("args: ", *args)
	println(list)
}
```

#### 3.4.3 값의 쌍 다루기: 중위 호출과 구조 분해 선언

- infix call (중위 호출): 일반적인 함수 호출 식을 간략하게 나타낸 방법. 인자가 하나뿐인 일반 메서드 or 확장 함수에만 사용 가능
- destructuring declaration (구조 분해 선언): js의 구조 분해 할당과 유사
```kotlin
val map = mapOf(1 to "one", 7 to "seven", 53 to "fifty-three")
1.to("one") // 확장 함수 to를 일반적인 방식으로 호출
1 to "one" // 중위 호출 

val (number, name) = 1 to "one" // 구조 분해 선언 number == 1, name == "one"
```

### 3.5 문자열과 정규식 다루기

#### 3.5.1 문자열 나누기

- 코틀린 정규식 문법은 자바와 같으며, 확장함수를 이용하여 더욱 간편하게 나타냄
```kotlin
println("12.345-6.A".split("\\.|-".toRegex())) // 정규식 이용
println("12.345-6+A".split('.', '-')) // 확장함수 이용
```

#### 3.5.2 정규식과 3중 따옴표로 묶은 문자열

- 3중 따옴표 문자열에서는 역슬래시를 포함한 어떤 문자로 이스케이프 필요없음
- 
```kotlin
fun main() {
	parsePath("/User/yole/kotlin-book/chapter.adoc")
}

fun parsePath(path: String) {
	val regex = """(.+)/(.+)\.(.+)""".toRegex() // (.+): 디렉터리, 파일이름, 확장자를 나타낸다
    val matchResult = regex.matchEntire(path)
    
    if(matchResult != null) {
        val (directory, filename, extension) = matchResult.destructured
        println("Dir: ${directory}, name: ${filename}, ext: ${extension}")
    }
}
```
### 3.6 코드 다듬기: 로컬 함수와 확장

- 코틀린에서는 함수에서 추출한 로컬 함수를 원 함수 내부에 중첩시켜 DRY(코드중복)를 지향

```kotlin
class User(val id: Int, val name: String, val address: String)

fun	User.validateBeforeSave() {
	fun validate(value: String, fieldName: String) { // 로컬함수 정의
		if(value.isEmpty()) {
			throw IllegalArgumentException("Can't save user ${id}: " + "empty $fieldName")
		}

	}
	// 로컬함수를 호출해서 각 필드를 검증
	validate(name, "Name")
	validate(address, "Address") 
}

fun saveUser(user: User) {
	user.validateBeforeSave() // 확장함수 호출
}
```