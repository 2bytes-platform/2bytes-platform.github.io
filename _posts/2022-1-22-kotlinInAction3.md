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
fun <T> collection<T> joinToString (
    separator: String = ", ",
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

- 