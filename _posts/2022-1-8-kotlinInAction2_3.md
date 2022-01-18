---
layout: post
title: "📅 Kotlin in Action - 2장 ③"
excerpt: "Kotlin in Action 2장 요약 노트입니다."
subtitle: "Kotlin in Action"
toc: true
toc_sticky: true
toc_label: "페이지 주요 목차"
date: 2022-1-8
tags: [Kotlin]
---

### 2.4 대상을 iteration: while과 for loop

- for는 자바의 for-each 루프에 해당하는 형태만 존재하며, 형태는 for <아이템> in <원소들>

#### 2.4.1 while 루프

- 자바와 비슷
```kotlin
// 조건이 참인 동안 본문을 반복 실행
while (조건) {
    /* 실행문*/
}

// 맨 처음에 무조건 본문을 한번 실행한 다음, 조건이 참인 동안 본문을 반복 실행
do {
    /* 실행문*/    
} while (조건)
```

#### 2.4.2 수에 대한 이터레이션: 범위와 수열

- 코틀린에는 자바의 for loop에 해당하는 요소가 없으며, 이에 범위(range)를 따로 지정
- 범위는 정수 등의 숫자 타입의 값이며 양끝을 포함
```kotlin
val oneToTwenty = 1..20
```
```kotlin
// when을 사용해 fizzBuzz 게임 구현하기
fun fizzBuzz(i: Int) = when {
    i % 15 == 0 -> "FizzBuzz"
    i % 3 == 0 -> "Fizz"
    i % 5 == 0 -> "Buzz"
    else -> "$i"
}
// 증가 값을 갖고 범위 이터레이션
for (i in 1..100) {
    print(fizzBuzz(i))
}
// downTo 1은 역방향 수열을 지정하며, step 2는 증가값(감소값)이 2(-2)를 뜻함 
for (i in 200 downTo 1 step 2) {
    print(fizzBuzz(i))
}
// until은 끝 값을 포함하지 않는다
for (i in 0 until size) {
    print(fizzBuzz(i))
}
```

#### 2.4.3 맵에 대한 이터레이션

- for loop를 사용해 이터레이션하려는 컬렉션의 원소를 풀 수 있음
```kotlin
val binaryReps = TreeMap<Char, String>() 
for (c in 'A'..'F') { // A부터 F까지 문자범위 사용
    val binary = Integer.toBinaryString(c.toInt()) // 아스키 코드를 2진 표현으로 변경
    binaryReps[c] = binary
}
for ((letter, binary) in binaryReps) {
    println("$letter = $binary")
    
}

// 객체를 표현하는 방법 2가지
binaryReps [c] = binary
binaryReps.put (c, binary)
```

#### 2.4.4 in으로 컬렉션이나 범위의 원소 검사

- in 연산자를 사용해 어떤 값이 범위에 속하는지 알 수 있음. !in 연산자를 사용해 반대의 경우도 확인 가능

```kotlin
fun isLetter(c: Char) = c in 'a'..'z' || c in 'A'..'Z'
fun isNotDigit(c: Char) = c !in '0'..'9'
```

```kotlin
// when에서 in 사용하기
fun recognize(c: Char) = when (c) {
    in '0'..'9' -> "It's a digit"
    in 'a'..'z', in 'A'..'Z' -> "It's a letter!"
    else -> "Fucked"
}
```
- 비교가 가능한 클래스라면 그 클래스의 인스턴스 객체를 사용해 범위 생성 가능

### 2.5 코틀린의 예외처리

- 발생한 예외를 함수 호출 단에서 catch하지 않으면 함수 호출 스택을 거슬러 올라가면서 예외를 처리하는 부분이
나올 때까지 예외를 다시 던짐

```kotlin
val percentage =
    if (number in 0..100)
        number
    else
        throw IllegalArgumentException (
            "A percentage value must be between 0 and 100: $number")
```
#### 2.5.1 try, catch, finally

- 자바와 마찬가지로 파일에서 각 줄을 읽어 수로 변환하되 그 줄이 올바른 수 형태가 아니면 null 반환
- 체크 예외 처리를 강제하는 자바와는 달리 코틀린은 자유로움
```kotlin
fun readNumber (reader: BufferReader) : Int? {
    try {
        val line = reader.readLine()
        return Integer.parseInt(line)
    }
    catch (e: NumberFormatException) {
        return null
    }
    finally {
        reader.close()
    }
}
```

#### 2.5.2 try를 식으로 사용

- 코틀린의 try 키워드는 식이므로 변수에 대입할 수 있고, 본문을 반드시 중괄호 {}로 둘러싸야함
- JS의 try catch 구문과 거의 유사
```kotlin
// try를 식으로 사용하기
fun readNumber(reader: BufferedReader) {
    val number = try {
        Integer.parseInt(reader.readLine()) // try 식의 값
    } catch (e: NumberFormatException) {
        return 
    }
    println(number)
}

// catch에서 값 반환하기
fun readNumber(reader: BufferedReader) {
    val number = try {
        Integer.parseInt(reader.readLine())
    } catch (e: NumberFormatException) {
        null // 예외가 발생하면 null값을 사용 
    }
}
```
