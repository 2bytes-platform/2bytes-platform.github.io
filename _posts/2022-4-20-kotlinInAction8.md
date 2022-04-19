---
layout: post
title: "📅 Kotlin in Action - 8장 고차 함수: 파라미터와 반환 값으로 람다 사용"
excerpt: "Kotlin in Action 8장 요약 노트입니다."
subtitle: "Kotlin in Action"
toc: true
toc_sticky: true
toc_label: "페이지 주요 목차"
date: 2022-4-20
tags: [Kotlin]
---

>목표: 고차 함수로 코드를 더 간결하게 다듬고 코드 중복을 없애는 등 더 나은 추상화를 구축하는 방법을 배워보자.


### 8.1 고차 함수 정의 

- 고차 함수: 다른 함수를 인자로 받거나 함수를 반환하는 함수, 코틀린에서는 람다나 함수 참조를 인자로 넘기거나 반환할 수 있음

#### 8.1.1 함수 타입

- 컴파일러는 sum과 action이 함수 타입임을 추론함 

```kotlin
    val sum: (Int, Int) -> Int = { x, y -> x + y } // Int 인자 2개를 받아서 Int 값을 반환 
    val action: () -> Unit = { println(42) } // No 인자, No 리턴 함수
```

- 함수 타입을 정의하려면 함수 인자의 타입을 괄호 안에 넣고, 그 뒤에 화살표를 추가한 다음, 함수의 반환 타입을 지정
- Unit 타입은 의미 있는 값을 반환하지 않음

```kotlin
(Int, String) -> Unit 
```

- 함수 타입에서도 반환 타입을 nullable 타입으로 지정 가능
- 마찬가지로 nullable 함수 타입 변수 정의 가능. 단, 함수 타입 전체가 nullable 선언하기 위해 함수 타입을 괄호로 감싸고 물음표 기재

```kotlin
var canReturnNull: (Int, Int) -> Int? = {x, y -> null}
var funOrNull: ((Int, Int) -> Int)? = null
```

- 인자명은 타입 검사 시 무시되며, 람다 정의 시, 인자명이 함수 타입 선언의 파라미터 이름과 일치하지 않아도 됨 

```kotlin
fun performRequest(
    url: String,
    callback: (code: Int, content: String) -> Unit
) {/*...*/}

val url = "https://2bytescorp.com"
performRequest(url) { code, page -> /*...*/ } // 2번째 인자명이 page로 설정되도 상관x
```

#### 8.1.2 인자로 받은 함수 호출 

