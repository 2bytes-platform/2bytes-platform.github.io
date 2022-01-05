---
layout: post
title: "📅 Kotlin in Action - 2장 요약"
excerpt: "Kotlin in Action 2장 요약 노트입니다."
subtitle: "Kotlin in Action"
toc: true
toc_sticky: true
toc_label: "페이지 주요 목차"
date: 2022-1-3
tags: [Kotlin]
---

### 2.1 기본 요소: 함수와 변수

#### 2.1.1 Hello, World!

```kotlin
fun main(args: Array<string>) {
    println("Hello, world!")
}
```
- 함수를 선언할 때에 fun 키워드를 사용
- 인자 뒤에 타입을 사용
- 함수를 최상위 수준에 정의할 수 있으며, 자바와 달리 꼭 클래스 안에 함수를 넣어야 할 필요가 없음
- 배열 처리를 위한 문법이 따로 존재하지 않음
- 표준 자바 라이브러리 함수를 간결하게 사용할 수 있게 감싼 래퍼를 제공. 덕분에 System.out.println 대신에 
println라고 간결하게 사용 가능 
- 세미콜론 생략가능

#### 2.1.2 함수

```kotlin
fun max(a: Int, b: Int): Int {
    return if (a > b) a else b
} // expression body: 식본문
println(max(1,2)) // 2

fun max(a: Int, b: Int): Int = if(a > b) a else b // block body: 블록본문
```
- 코틀린에서 if는 자바와 다르게 값을 만들어 내며 다른 식의 하위 요소로 계산에 참여할 수 있는 expression임.
참고로 statement는 자신을 둘러싸고 있는 가장 안쪽 블록의 최상위 요소이며, 어떤 값도 만들어내지 않음


- type inference(타입추론): 식이 본문인 함수의 경우 반환 타입을 적지 않아도 컴파일러가 함수 본문 식을 분석해
결과 타입을 함수 반환 타입으로 정해주는 것을 뜻함. 식본문 함수에서만 타입 생략 가능

#### 2.1.3 변수


- var: 변경 가능한 참조를 저장하는 변수. 자바의 일반 변수와 같다. 변수의 값을 변경할 수 있지만 변수의 
타입은 고정돼 바뀌지 않는다.
- val: 변경 불가능한 참조를 저장하는 변수. 초기화 후 재할당은 불가하지만 객체의 내부 값은 변경 가능함.
자바의 final 변수와 같다.
 
```kotlin
val languages = arraylistOf("Java") 
languages.add("Kotlin") // true

var anwer = 42
answer = "no answer" // Error: type mismatch
```

#### 2.1.4 더 쉽게 문자열 형식 지정: 문자열 템플릿
- 문자열 리터럴 안에서 변수를 사용하기 위해서는 '$'를 앞에 붙여주자
- 문자열 템플릿 안에는 간단한 변수뿐만이 아니라 식도 들어갈 수 있으므로 가능하면 '${변수 or 식}' 형태로 이용  
- 또한 '$'를 특수문자로 쓰고 싶다면 '\'를 이용하여 escape 시키면 가능

```kotlin
fun main(args: Array<String>) {
    if (args.size > 0) {
        println("Hello, ${args[0]}")
    }
}

fun main(args: Array<String>) {
    println("Hello, ${if (args.size > 0) args[0] else "someone"}!")
} //템플릿 리터럴 안에서 쌍따옴표도 사용 가능

```

### 2.2 클래스와 프로퍼티
- 간단한 자바빈 클래스인 Person을 정의했으며, name 이라는 프로퍼티만 들어있음
```java
public class Person {
    private final String name;
    public class Person(String name) {
        this.name = name;
    }
    public String getName() {
        return name;
    }
}
```
- 코틀린으로 치환한 코드이며 코드량이 적어진 것을 확인할 수 있음. 이렇게 코드없이 데이터만 저장하는 클래스를
value object(값 객체)라 부름
```kotlin
class Person(val name: String)
```
#### 2.2.1 프로퍼티

```kotlin
class Person(
    val name: String, // 읽기 전용 프로퍼티, 코틀린은 필드와 게터 생성
    val isMarried: Boolean // 쓸 수 있는 프로퍼티, 필드와 세터 그리고 게터 생성 
)

val person = Person("Bob", true)
println(person.name) // Bob
println(person.isMarried) // true
```
> 필드: 데이터를 저장하는 곳  
> 게터: 필드를 읽는 것   
> 세터: 필드를 변경하는 것 
> accessor method (접근자 메소드): 클라이언트가 클래스를 통해서 데이터에 접근할 수 있게 제공하는 통로

- 자바에서는 필드와 접근자를 묶어 프로퍼티라고 부르며, 코틀린은 기본 기능으로 제공하며 필드와 접근자를 완전히 대신함

#### 2.2.2 커스텀 접근자

```kotlin
class Rectangle(val height: Int, val width: Int) {
    val isSquare: Boolean
    get() { //프로퍼티 게터 선언
        return height == width
    }
}

val rectangle = Rectangle(41, 43)
println(rectangle.isSquare) // false
```

- get(): 커스텀 프로퍼티 접근자이며, 클라이언트가 해당 접근자를 이용하여 프로퍼티 값을 계산


