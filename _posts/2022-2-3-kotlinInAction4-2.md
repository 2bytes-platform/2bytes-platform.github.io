---
layout: post
title: "📅 Kotlin in Action - 4장 클래스, 객체, 인터페이스"
excerpt: "Kotlin in Action 4장 요약 노트입니다."
subtitle: "Kotlin in Action"
toc: true
toc_sticky: true
toc_label: "페이지 주요 목차"
date: 2022-2-3
tags: [Kotlin]
---

#### 4.2.4 게터와 세터에서 뒷받침하는 필드에 접근 

- 특정 값을 저장하되 그 값을 변경하거나 읽을 때마다 정해진 로직을 실행하는 유형의 프로퍼티를 생성

```kotlin
fun main() {
    val user = User("Alitciia")
    user.address = "서울시 송파구 토성로 15길 10-1 바움빌 401호" 
    println(user) 
    println(user.address)
}

class User(val name: String) {
    var address: String = "unspecified"
    	set(value: String) {
            println("""
            	Address was changed for $name:
   				"$field" -> "$value".""".trimIndent())
            field = value
        }
}
```

#### 4.2.5 접근자의 가시성 변경

- 접근자의 가시성은 기본적으로 프로퍼티의 가시성과 같으나 get, set 앞에 가시성 변경자를 추가해서 접근자 가시성 변경 가능

```kotlin
fun main() {
	val lengthCounter = LengthCounter()
	lengthCounter.addWord("Hi!")
	println(lengthCounter.counter) // 3
}

class LengthCounter {
	var counter: Int = 0
		private set
	fun addWord(word: String) {
		counter += word.length
	}
}
```

### 4.3 컴파일러가 생성한 메서드: 데이터 클래스와 클래스 위임

- 코틀린 컴파일러가 데이터 클래스에 유용한 메서드를 자동으로 만들어주는 예와 클래스 위임 패턴을 보여주는 예를 보자

#### 4.3.1 모든 클래스가 정의해야 하는 메서드 

- 클래스에 기본적으로 들어있는 메서드들을 커스터마이징 

```kotlin
fun main() {
	val client1 = Client("사샤", 4122)
    println(client1) // Client(name = 사샤, postalCode=4122)
}

class Client (val name: String, val postalCode: Int) {
	override fun toString() = "Client(name = $name, postalCode=$postalCode)"   
}
```

- 객체의 동등성: equals(other: Any)
> 
> "=="는 원시 타입일 경우 피연산자의 값이 같은지를 비교, 참조 타입인 경우 피연산자의 주소가 같은지를 비교. 코틀린에서 
> "=="는 내부적으로 equals를 호출해서 객체 비교

```kotlin
fun main() {
	val client1 = Client("오현석", 4122)
    val client2 = Client("오현석", 4122)
    println(client1 == client2) // false
}

class Client (val name: String, val postalCode: Int) {
	override fun toString() = "Client(name = $name, postalCode=$postalCode)"   
}
```

```kotlin
class Client(val name: String, val postalCode: Int) {
	override fun equals(other: Any?) : Boolean {
		if (other == null || other !is Client)
			return false
		return name == other.name && postalCode == other.postalCode
	}
	override fun toString() = "Client(name = $name, postalCode=$postalCode)"
}
```

#### 4.3.2 데이터 클래스: 모든 클래스가 정의해야 하는 메소드 자동 생성 

- data라는 변경자를 클래스 앞에 붙이면 필요한 메서드를 컴파일러가 자동으로 만들어줌. 그리고 이러한 클래스를 데이터 클래스라고 함
- 하기 클래스는 다음과 같은 메서드를 포함. 인스턴스 비교를 위한 equals, 해시 기반 컨테이너에서 키로 사용할 수 있는 hashCode, 클래스의 각 필드를
선언 순서대로 표시하는 문자열 표현을 만들어 주는 toString 

```kotlin
data class Client(val name: String, val postalCode: Int) 
```

