---
layout: post
title: "📅 Kotlin in Action - 4장 함수 정의와 호출"
excerpt: "Kotlin in Action 4장 요약 노트입니다."
subtitle: "Kotlin in Action"
toc: true
toc_sticky: true
toc_label: "페이지 주요 목차"
date: 2022-1-24
tags: [Kotlin]
---

### 4.1 클래스 계층 정의 

#### 4.1.1 코틀린 인터페이스

- 코틀린 인터페이스 안에는 추상 메서드 뿐만 아니라 구현이 있는 메서드도 정의 가능 
- override 변경자는 실수로 상위 클래스의 메서드를 오버라이드 하는 것을 방지
- 상위 타입의 이름을 꺽쇠 괄호 사이에 넣어서 super를 지정하면, 어떤 상위 타입의 멤버 메서드를 호출할지 지정 가능

```kotlin
fun main(args: Array<String>) {
	val button = Button()
    button.showOff() //  I'm clickable! I'm Focusable!
    button.setFocus(true) // I got focus.
    button.click() // I was clicked!
}

interface Clickable {
	fun click() // 일반 메서드 선언
	fun showOff() = println("I'm clickable!") // 디폴트 구현이 있는 메서드
}

interface Focusable {
	fun setFocus(b: Boolean) = println("I ${if (b) "got" else "lost"} focus.")
	fun showOff() = println("I'm Focusable!")
}


class Button: Clickable, Focusable {
	override fun click() = println("I was clicked!")
	override fun showOff(){ 
		super<Clickable>.showOff()
		super<Focusable>.showOff() // 
	}
}
```

#### 4.2.2 open, final, abstract 변경자: 기본적으로 final

- 하위 클래스에서 오버라이드하게 의도된 클래스와 메서드가 아니라면 모두 final class로 만들 것 